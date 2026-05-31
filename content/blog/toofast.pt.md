---
title: "Construí o Deploy Tracker rápido demais"
date: 2026-05-31
translationKey: deploy-tracker-too-fast
description: "O que o Deploy Tracker me ensinou sobre avançar rápido demais, empilhar ferramentas antes dos fundamentos e voltar para Linux, redes e bases de sistemas."
tags:
  - deploy-tracker
  - devops
  - linux
  - networking
  - observability
  - docker
---

O Deploy Tracker não foi um fracasso. Foi um espelho. Ele me mostrou que eu conseguia construir algo maior que um CRUD, mas também mostrou que eu estava empilhando ferramentas antes de treinar os fundamentos por trás delas.

<!--more-->

## O que o Deploy Tracker deveria ser

O Deploy Tracker deveria ser um dashboard de monitoramento de deploys com observabilidade.

A ideia era simples: registrar aplicações, monitorar a saúde delas, coletar métricas, exibir status, mostrar logs e disparar alertas quando houvesse downtime.

Repositório: [Deploy Tracker](https://github.com/MuriloCosta29/deploy-tracker)

Quando comecei o Deploy Tracker, eu tinha dois objetivos principais:

1. Sair dos projetos CRUD básicos.
2. Chegar mais perto das ferramentas usadas no mundo DevOps.

Por isso escolhi tecnologias como FastAPI, PostgreSQL, Redis, Celery, Prometheus, Grafana, Docker Compose, GitHub Actions e Nginx.

Na época, parecia o próximo passo certo.

E, de certa forma, foi.

## O que acertei

Duas coisas importantes.

1. Aprendi muito com esse projeto, e não me arrependo de ter construído. Por causa do Deploy Tracker, encontrei problemas que poderiam aparecer muito mais tarde na minha jornada, mesmo que alguns deles fossem básicos.
2. Sei que, em programação, nunca vou saber tudo. Então não devo deixar uma pequena lacuna de conhecimento me impedir de terminar um projeto. Nesse caso, o problema era diferente: percebi que o que eu não sabia não era apenas um detalhe pequeno. Era parte da base. E uma base forte é essencial.

O problema real não era FastAPI, Redis, Celery, Docker, Prometheus ou Grafana.

O problema era que eu estava usando ferramentas construídas em cima de fundamentos que eu ainda não tinha treinado o suficiente.

Como eu não entendia HTTP com profundidade suficiente, FastAPI parecia mais fácil do que realmente era.

- Eu conseguia criar rotas, mas não conseguia explicar completamente o que acontecia entre um cliente enviar uma requisição e a API retornar uma resposta.
- Eu conseguia ler o Swagger, mas não entendia profundamente headers, status codes, request bodies, query parameters e path parameters.

Como eu não entendia redes com profundidade suficiente, Docker Compose e Nginx escondiam detalhes importantes de mim.

- Eu conseguia rodar vários containers, mas não entendia completamente como eles se comunicavam.
- Eu usava portas, nomes de serviço e `localhost`, mas não entendia a diferença entre `localhost` na minha máquina e `localhost` dentro de um container.
- Eu adicionei Nginx como reverse proxy, mas não entendia completamente o que acontecia quando uma requisição era encaminhada para a API.

Como eu não entendia processos e serviços Linux com profundidade suficiente, Celery parecia mágica.

- Eu conseguia rodar um worker e um beat scheduler, mas não entendia completamente o que um processo worker estava fazendo.
- Eu usava background jobs, mas precisava entender melhor processos, signals, serviços e tratamento de falhas.
- O problema do health check hardcoded me mostrou que eu estava fazendo o sistema rodar sem pensar direito em como o workflow deveria se comportar.

Como eu não entendia cache com profundidade suficiente, Redis virou só mais uma ferramenta na stack.

- Eu sabia que Redis podia deixar leituras mais rápidas, mas precisava entender cache invalidation, TTL, stale data e o que deveria acontecer quando o Redis ficasse indisponível.
- Eu usei Redis, mas não entendia completamente os problemas operacionais que vêm junto com cache.

Como eu não entendia observabilidade com profundidade suficiente, Prometheus e Grafana ficaram mais sobre dashboards do que diagnóstico.

- Eu expus métricas e criei um dashboard no Grafana, mas ainda precisava entender o que torna uma métrica útil.
- Eu precisava entender a diferença entre logs, metrics, traces, dashboards e alerts.
- Eu conseguia ver gráficos, mas ainda não estava pronto para desenhar observabilidade a partir dos primeiros princípios.

Como eu não entendia configuração e deploy com profundidade suficiente, algumas partes do projeto ficaram presas demais ao meu ambiente local.

- Usei valores hardcoded onde a configuração deveria ser explícita.
- Não separei bem configurações de desenvolvimento local de configurações mais próximas de produção.
- Eu precisava entender por que `.env.example`, secrets, environment variables e configuração de serviços importam.

A maior lição é esta:

Eu conseguia fazer o sistema rodar, mas não conseguia explicar cada camada importante que fazia ele funcionar.

## O erro

O erro não foi construir o Deploy Tracker.

O erro foi construí-lo rápido demais.

Eu empilhei ferramentas avançadas antes de treinar os fundamentos dos quais essas ferramentas dependem. Eu estava aprendendo a conectar serviços, mas nem sempre entendia as camadas por baixo deles.

Isso é perigoso, especialmente para alguém que quer se tornar DevOps ou Platform Engineer.

Em backend, entender os fundamentos já é importante. Em DevOps e Platform Engineering, isso é ainda mais importante, porque o trabalho não é apenas escrever código. O trabalho é entender sistemas, falhas, ambientes de deploy, redes, serviços, logs, métricas, confiabilidade e infraestrutura.

Se eu não entendo a base, ainda consigo copiar comandos, rodar containers, expor dashboards e fazer um projeto parecer impressionante.

Mas quando algo quebra, eu não sei onde olhar primeiro.

Esse era o problema real.

## Quando percebi isso

Comecei a perceber o problema enquanto trabalhava com FastAPI.

No começo, criar endpoints parecia simples. Eu conseguia definir uma rota, abrir o Swagger, enviar uma requisição e receber uma resposta.

Mas então vi métodos HTTP como `GET`, `POST`, `PATCH` e `DELETE`, e me peguei pensando:

> O que exatamente é um método HTTP?

Essa pergunta me incomodou.

Não porque perguntar isso fosse ruim, mas porque mostrou que eu estava usando um framework web antes de entender o suficiente sobre o protocolo por trás dele.

Eu conseguia escrever:

```python
@router.get("/applications")
```

Mas não conseguia explicar completamente o que acontecia desde o momento em que um cliente enviava aquela requisição até o momento em que o FastAPI retornava uma resposta.

Depois, o mesmo padrão começou a aparecer em outras partes do projeto.

Eu conseguia rodar containers com Docker Compose, mas não entendia profundamente redes entre containers.

Eu conseguia adicionar Nginx, mas não entendia completamente o comportamento de um reverse proxy dentro de uma rede Docker.

Eu conseguia rodar Celery, mas não entendia profundamente workers, filas, comportamento de processos, retries e tratamento de falhas.

Eu conseguia expor métricas do Prometheus e construir um dashboard no Grafana, mas ainda estava aprendendo a diferença entre observabilidade real e apenas ter gráficos em uma tela.

O projeto funcionava.

Mas funcionar não é a mesma coisa que entender.

## Por que isso importa

Por muito tempo, achei que chegar mais perto de DevOps significava usar mais ferramentas de DevOps.

- Docker.
- Redis.
- Celery.
- Prometheus.
- Grafana.
- Nginx.
- CI/CD.

Essas ferramentas importam, mas elas não são a base.

A base é entender o que acontece por baixo:

- Como HTTP funciona.
- Como processos rodam.
- Como serviços se comunicam.
- Como portas e sockets funcionam.
- Como Linux representa informações do sistema.
- Como logs são produzidos e consumidos.
- Como métricas descrevem o comportamento de um sistema.
- Como background jobs falham.
- Como configuração entra em uma aplicação.
- Como ambientes de deploy diferem do desenvolvimento local.

DevOps e Platform Engineering não são sobre colecionar ferramentas no currículo.

São sobre entender sistemas bem o suficiente para construir, rodar, debugar e melhorar esses sistemas.

O Deploy Tracker me ensinou que eu estava tentando subir alto demais sem verificar se a base era forte o suficiente.

## Como estou corrigindo isso

Para corrigir isso, criei outro projeto: System Monitor.

System Monitor é uma ferramenta de monitoramento de sistema Linux escrita em C.

O objetivo não é usar ferramentas avançadas. O objetivo é entender melhor o sistema operacional lendo informações diretamente de interfaces do Linux como `/proc`, `/etc/passwd`, `/var/log` e system calls.

Com esse projeto, quero estudar:

- Processes
- Signals
- Users and groups
- File permissions
- Filesystem metadata
- CPU usage
- Memory usage
- Disk usage
- Network connections
- Logs
- Environment variables
- `systemd`
- Cron jobs
- Terminal UI com `ncurses`

Isso não é tão chamativo quanto um dashboard com Prometheus e Grafana.

Mas está mais perto da base de que preciso.

Se eu quero me tornar DevOps ou Platform Engineer, preciso entender Linux, redes, serviços e comportamento de sistemas. Não apenas as ferramentas construídas em cima disso.

## O que vem depois

Não estou abandonando o Deploy Tracker.

Estou dando um passo para trás para poder voltar a ele com mais maturidade.

Depois de construir uma base mais forte com o System Monitor, quero voltar ao Deploy Tracker e reconstruir partes dele com uma compreensão mais profunda dos sistemas por trás.

Algumas coisas que quero revisitar:

- O workflow de health checks.
- O scheduler do Celery.
- Redes no Docker Compose.
- Configuração do reverse proxy com Nginx.
- Configuração baseada em ambiente.
- Testes para os fluxos de aplicação e health check.
- Responsabilidades de CI/CD.

Também quero escrever posts individuais sobre as ferramentas que usei no Deploy Tracker:

- Celery
- Prometheus
- Grafana
- GitHub Actions
- CI/CD
- Docker Compose
- Nginx

Mas, desta vez, não quero escrever apenas sobre como usei essas ferramentas.

Quero escrever sobre por que elas existem, qual problema resolvem, de quais fundamentos dependem e o que eu entendi errado quando usei pela primeira vez.

## Pensamentos finais

O Deploy Tracker não foi um fracasso.

Foi um espelho.

Ele me mostrou que consigo construir projetos, conectar ferramentas e terminar algo maior que um CRUD.

Mas também mostrou que ambição sem fundamento pode me fazer andar rápido demais na direção errada.

Essa é a verdadeira lição.

Não me arrependo de ter construído o Deploy Tracker.

Fico feliz por ter construído.

Porque agora sei o que preciso corrigir.
