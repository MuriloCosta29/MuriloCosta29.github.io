---
title: "Adicionando Redis ao Deploy Tracker — e o que cache realmente resolve"
date: 2026-04-28
translationKey: redis-deploy-tracker-caching
description: "Como adicionei cache Redis a uma aplicação FastAPI usando o padrão cache-aside — e o bug de serialização JSON que me ensinou a ler os logs."
tags:
  - redis
  - fastapi
  - postgresql
---

Adicionei Redis ao Deploy Tracker usando o padrão cache-aside. O objetivo era simples: evitar consultas repetidas ao PostgreSQL quando os mesmos dados fossem solicitados várias vezes.

<!--more-->

## O problema

- Toda vez que um `GET` busca dados no PostgreSQL, existe um custo. Se os dados mudaram, tudo bem: faz sentido consultar novamente. Mas **se os dados não mudaram?** Aí existe trabalho repetido, e o Redis entra para resolver isso.

## Por que Redis

- Uma variável Python não tem expiração automática. Ela também desaparece quando o processo reinicia e não é compartilhada entre múltiplos workers. Redis resolve esses problemas porque é um serviço separado e consegue expirar chaves automaticamente com TTL.
- Redis armazena dados em RAM, o que torna a resposta mais rápida, porque buscar na memória é muito mais rápido do que buscar no disco.
- Quando você é iniciante, é comum pensar: "Por que eu usaria um message broker/database como Redis só para deixar um pouco mais rápido?" Mas lendo "Grokking Algorithms", percebi uma coisa: se você é **iniciante**, não olhe só para o tamanho atual do seu projeto. Pegue uma parte dele e imagine: "E se isso tivesse 1.000 usuários? Ou 1.000.000? Continuaria rodando bem ou ficaria lento?"
- Cache não é só deixar uma requisição mais rápida. É evitar trabalho repetido quando a resposta já é conhecida.

## Como implementei

**1.** Para implementar Redis, criei o `cache.py`, responsável pelas operações de cache.

```python
def get_cache(key):
    value = r.get(key)
    if value is not None:
        new_value = json.loads(value)
        return new_value

    return None


def to_dict(obj):
    return {c.name: getattr(obj, c.name) for c in obj.__table__.columns}


def set_cache(key, data):
    data = [to_dict(item) for item in data]
    value = json.dumps(data, default=str)
    r.set(key, value, ex=300)


def delete_cache(key):
    r.delete(key)
```

**2.** `GET /applications` antes e depois do Redis.

Sem Redis, apenas banco de dados:

```python
@router.get("/applications")
def list_applications(db: Session = Depends(get_session)):
    return db.query(Application).all()
```

Com Redis integrado:

```python
@router.get("/applications")
def list_applications(db: Session = Depends(get_session)):
    cached = get_cache("applications_all")
    if cached:
        return cached
    applications = db.query(Application).all()
    set_cache("applications_all", applications)
    return applications
```

**Importante:** quando os dados mudam, o cache precisa ser invalidado para evitar resultados desatualizados. Por exemplo, depois de criar ou atualizar uma aplicação, preciso chamar `delete_cache("applications_all")`.

## Invalidação de cache — quando os dados mudam com POST/PATCH/DELETE

Invalidação de cache é um problema chato. Ela acontece porque os dados no banco mudam, mas os dados no cache não. Isso cria inconsistência, também chamada de stale data.

- Banco de dados -> dados originais
- Cache -> cópia dos dados

Para resolver isso, apaguei a chave em cache toda vez que o dado original mudava.

Então depois de `POST`, `PATCH` ou `DELETE`, a API chama:

```python
delete_cache("applications_all")
```

O próximo `GET /applications` vira um cache miss, consulta o PostgreSQL novamente e salva o resultado atualizado no Redis.

## O bug que me surpreendeu

Quando implementei Redis, tentei salvar objetos SQLAlchemy diretamente no cache.

Para minha surpresa, a API retornou `500 Internal Server Error`.

No começo, perguntei: "O que fiz errado?" Mas a pergunta mais importante era: "Como eu identifico o bug?"

Nesse caso, minha IDE não mostrou nada útil. Então fui olhar os logs do terminal.

Essa foi uma lição importante: às vezes o erro não aparece no editor. A aplicação está rodando, o código parece certo, mas a explicação real está nos logs.

Depois de ler os logs, encontrei o problema: `json.dumps` não conseguia serializar objetos SQLAlchemy.

Foi aí que entendi o erro. Redis não estava armazenando meus objetos Python diretamente. Nesta implementação, eu precisava converter meus models SQLAlchemy em dicionários antes de salvar no cache.

Então criei o helper `to_dict()`:

```python
def to_dict(obj):
    return {c.name: getattr(obj, c.name) for c in obj.__table__.columns}
```

Meu segundo problema foi com `created_at`. Eu uso `datetime.datetime` para salvar a data, mas `json.dumps()` só entende tipos como:

```text
dict
list
str
int
float
bool
None
```

Então como `json.dumps()` transforma um objeto do módulo `datetime` em string?

Para resolver, usei:

```python
value = json.dumps(data, default=str)
```

Isso basicamente significa: se encontrar um objeto que não sabe serializar, converta para string.

Por causa disso, no Deploy Tracker o `created_at` vira algo como `"2026-04-19 23:59:59"` em formato de string.

Importante: Redis não estava exigindo JSON especificamente. Eu usei JSON como formato para transformar meus dados Python em uma string antes de salvar no Redis.

## O que aprendi

1. **PostgreSQL** -> disco -> mais lento | **Redis** -> RAM -> mais rápido
2. Velocidade pode parecer opcional no começo, mas com muitos dados até um pequeno atraso faz diferença.
3. Cache parece simples, mas cria uma nova responsabilidade: manter o cache consistente com o banco.
4. **O banco de dados é a fonte da verdade.** Redis guarda uma cópia temporária.
5. **Logs fazem parte do debugging.** Minha IDE não mostrou o problema real, mas os logs explicaram por que a API retornava `500`.
6. Redis armazena strings/bytes.
