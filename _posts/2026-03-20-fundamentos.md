---
layout: post
title: "O que eu não sabia antes de usar FastAPI"
date: 2026-03-20
---
Olá, um breve aviso! Enquanto eu estava escrevendo o 3º Post sobre FastAPI na prática, eu percebi que tinha algumas coisas que eu não sabia realmente o que significavam e enquanto eu escrevia sobre a FastAPI, eu fui anotando essas coisas que eu não sabia e fui procurar o significado delas para de fato entender o que elas eram.

## Começando...
**1º - O que é um Framework?** Na criação de um site, aplicativo ou sistema complexo, desenvolver TUDO do zero pode ser uma perda de tempo e um convite para falhas de segurança. É para resolver esses problemas que o Framework existe! Ele é um conjunto de códigos, ferramentas e boas práticas que atua como um 'esqueleto' para os desenvolvedores. Assim, em vez de construírem tudo do começo, os programadores já contam com uma estrutura sólida e pré-configurada como ponto de partida para criar suas aplicações.
- **Ferramentas:** Códigos prontos para resolver problemas comuns.  

- **Boas Práticas:** Para o projeto não virar uma bagunça, o Framework te obriga ou te incentiva a seguir separando códigos como, Model(Banco de Dados), View/Controller(Processamento de Lógica) entre outras regras de organização e Segurança.  


**Importante!!! 👇**  

**Framework web** - Estrutura Criada exclusivamente para construir aplicações que funcionam na internet.  (Em relação ao FastAPI)  

- Nem todo framework é um framework web, mas todo framework web é um framework.


## Bibliotecas Independentes
**Starlette** - Fundação ágil que recebe e roteia as requisições da internet.  
**Pydantic** - Camada de segurança que valida os dados de forma automática  

<mark>Juntas, formam a base perfeita para construir APIs modernas.</mark>  

- O FastAPI é baseado nessas duas bibliotecas supracitadas.


## API
**APIs** - Significa **Application Programming Interface** (Interface de Programação de Aplicações). É um mensageiro que permite que dois sistemas de software conversem entre si de forma segura padronizada e sem expor seus dados internos.  
- As APIs são muito importantes por conta da padronização! O que eu quero dizer com isso?  
- Quando eu estou criando algo e quero usar no `Front-end: JavaScript | Back-end: Python | Aplicativo: Swift.` As APIs faz com que essas linguagens conversem entre si. Hoje no dia desse post, o rei absoluto dessa padronização na web se chama **JSON** (JavaScript Object Notation).  

   **JSON** - texto simples e organizado, que agrupa os dados em pares de "Nome" e "Valor". Como ele é um padrão adotado mundialmente, um servidor em Python consegue gerar um texto em JSON, e o seu celular consegue ler e entender esse mesmo texto instantaneamente.  

## API REST

**APIs REST** - Toda API REST é uma API, mas nem toda API é REST. **REST** Significa: Representational State Transfer (Transferência de Estado Representacional). Uma API só ganha o "sobrenome" REST se o desenvolvedor construí-la seguindo um manual de regras muito rigoroso.
- **Uso correto do protocolo HTTP**: Uma API REST não inventa moda. Ela usa os verbos padrão da internet para cada ação.
  - `GET` - para buscar uma informação (ex: Pegar uma tarefa em um inbox)
  - `POST` - para criar algo novo (ex: criar uma tarefa para inbox)
  - `PUT` - para atualizar algo (ex: editar tarefa no inbox)
  - `PATCH` - para atualizar apenas uma parte específica de algo
  - `DELETE` - para apagar  

  Diferença entre `PUT` e `PATCH`:
  - **PUT (Substituição Total)** - Exemplo, se minha tarefa no inbox tem *Título, Descrição e Data*, E eu quero apenas mudar a data, eu preciso colocar título e descrição de novo.
  - **PATCH (Substituição Específica)** - Já no PATCH, pegando o gancho do exemplo passado, ele mudaria apenas a data! Sem eu precisar ter que reescrever descrição e título novamente.

## Estruturas Adicionais
**Template Engine** - É uma ferramenta de desenvolvimento web que permite criar páginas HTML dinâmicas, combinando modelos (templates) com dados reais. 

**Microserviços** - Microsserviços são uma abordagem arquitetônica de software que divide uma aplicação grande em pequenos serviços independentes, focados em funções específicas e que se comunicam entre si, geralmente via APIs.

Template Engine e Microserviços foram dois dos fatores que corroboraram para a escolha do FastAPI — e vou explicar mais no próximo post.
