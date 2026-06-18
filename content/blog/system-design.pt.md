---
title: "O que aprendi sobre System Design construindo o Deploy Tracker"
date: 2026-06-18
translationKey: deploy-tracker-system-design
description: "O que construir o Deploy Tracker me ensinou sobre System Design: por que não existe a melhor stack, apenas o contexto certo, e por que trade-off é a palavra-chave por trás de toda escolha arquitetural."
tags:
  - deploy-tracker
  - devops
  - system-design
---

Quando terminei o Deploy Tracker, ele funcionava — mas eu não conseguia explicar por que tinha escolhido cada ferramenta. Redis ou RabbitMQ? Celery ou ARQ? Eu tinha respostas, mas não tinha motivos. Essa lacuna tinha um nome que eu ainda não conhecia: System Design.

<!--more-->

## Como entrei em System Design

System Design não veio à minha cabeça do nada. Eu assisto vídeos do [Augusto Galego](https://www.youtube.com/watch?v=EWzVZA_qTEw), CTO de uma empresa fora do Brasil e um programador muito afiado. (Se quiser assistir ao vídeo e conhecer o canal dele, clique no nome.)

Começou quando eu estava rolando minha timeline do YouTube e encontrei um vídeo dele falando sobre System Design. Modéstia à parte, sou alguém que quer ser o melhor programador que eu puder ser — então fui pesquisar sobre isso. Mas percebi que ainda não era o momento certo para estudar esse assunto, e o Augusto falou algo parecido no vídeo.

Então deixei para depois. Tempos depois, fui escrever o README do Deploy Tracker e, quando cheguei na parte de explicar por que escolhi cada ferramenta, percebi que eu não conseguia explicar de verdade o motivo por trás das escolhas. Isso me incomodou. E, do nada, veio aquele momento típico:

"Ah — isso é System Design."

Depois disso, comecei a pesquisar: se eu soubesse System Design, como eu teria aplicado isso ao Deploy Tracker?

## O que aprendi sobre ferramentas

Para construir um projeto, não existe a ferramenta certa; existe o contexto certo.

Quando eu "escolhi" minhas ferramentas para o Deploy Tracker, eu não comparei opções de verdade. Por exemplo, para o message broker eu usei Redis, mas também poderia ter usado RabbitMQ.

O mesmo aconteceu com o worker assíncrono: usei Celery, mas ARQ também era uma opção.

Mas aqui está o ponto: mesmo que eu não tenha escolhido essas ferramentas por design, usá-las me ensinou conceitos reais como cache, filas e workers assíncronos.

##### Uma percepção no meio do projeto

Em algum momento do projeto — não lembro exatamente como — encontrei RabbitMQ e considerei usá-lo, porque vi que era o padrão de mercado e provavelmente seria melhor para mim.

Para minha surpresa, vi que Redis + ARQ é a "melhor dupla".

- "melhor dupla" entre aspas porque -> a melhor stack não existe. Existe um contexto melhor.

Então pesei as opções:

Para o message broker:

| Redis | RabbitMQ |
| :--- | :---: |
| Leve | Rico em recursos |
| Caso mais simples | Caso complexo |

Para o worker assíncrono:

| Celery | ARQ |
| :--- | :---: |
| Padrão de mercado | Não é padrão de mercado |
| Mais configuração para integrar com Redis | Construído em cima do Redis, integração mais simples |

Depois de pesar isso, decidi que usaria Redis porque ele se encaixa em um caso mais simples (que é a minha situação), e eu também vou aprender cache, que é o objetivo.

Para o worker assíncrono, Celery é o padrão de mercado, e isso é suficiente para mim.

Para concluir, eu entendo a escolha dessa arquitetura, e para o meu caso ela realmente é a melhor.

## Os três níveis

Chamei esta seção de "Os três níveis" por causa de: Júnior, Pleno e Sênior.

Quando comecei a estudar System Design para este projeto, perguntei a uma IA como System Design se aplicava a ele, e ela trouxe esses níveis. Achei isso muito interessante — então aqui está meu entendimento atual, como júnior. Eu ainda não vivi os níveis pleno e sênior, então leia a próxima parte como a forma como imagino que funciona, não como um fato.

**Júnior / Estagiário.** Para alguém começando, essa stack completa é a melhor opção, porque força você a estudar cache, tarefas em background e filas. Você termina o projeto com mais ferramentas e conhecimento para a carreira. Esse foi o meu caso.

**Pleno.** Um dev pleno provavelmente já conhece esses conceitos e quer aplicá-los — às vezes até fazendo over-engineering. Mas, se for maduro, imagino que tentaria reduzir o número de ferramentas para manter as coisas mais simples. (Sinceramente, ainda não sei exatamente quais ferramentas um pleno cortaria — isso é só meu chute.)

**Sênior.** Um sênior provavelmente quer o menor estresse operacional possível 😂, e usaria o mínimo de ferramentas necessário. No Deploy Tracker, imagino que um sênior talvez usasse o BackgroundTasks do FastAPI em vez do Celery, e para o banco de dados, algo como AWS RDS (Relational Database Service) — que descobri recentemente e achei interessante, porque suporta PostgreSQL, MySQL e outros.

## Trade-off

Mais uma vez, citando o [Galego](https://www.youtube.com/@GutoGalego) — aprendi essa palavra com ele.

Quando ouvi essa palavra, fui pesquisar seu significado. No começo, sendo sincero, eu não entendi, mas quando entendi, pareceu se encaixar em tudo — e em System Design ainda mais.

Se você pesquisar a definição de System Design no Google, encontra isto:

> "o processo de definir a arquitetura, os componentes, os fluxos de dados e as interfaces de um sistema de software para atender requisitos funcionais e de negócio específicos."

É por isso que tudo aqui aponta para TRADE-OFF. Se você quer definir arquitetura, componentes, fluxos de dados e interfaces para alcançar o projeto mais eficiente possível, precisa escolher uma coisa e descartar outra — como "Redis ou RabbitMQ?", "Celery ou ARQ?", ou "descartar os dois e usar apenas o BackgroundTasks do FastAPI com AWS RDS". Isso é trade-off puro. Você abre mão de recursos extras de que não precisa de verdade em troca de mais simplicidade, estabilidade e eficiência.

## O que muda para mim agora

Para mim, System Design tem o poder de fazer você entender o código com mais profundidade — a arquitetura e o que acontece por baixo dos panos.

Gosto de como isso se conecta com minha ideia de entender o código "completamente".

- Completamente = entender o fluxo do código.

Como eu disse no meu último post, construí o Deploy Tracker rápido demais — e rápido demais significou fazer funcionar sem entender o projeto completamente.

Isso me faz investir mais nos fundamentos da programação: C, ponteiros, memória, estruturas de dados e mais base. System Design me mostrou uma verdade interessante: se você está no começo da sua jornada em programação, não colecione ferramentas. No futuro, você só vai usar uma ferramenta se ela for realmente necessária. Você não usa uma ferramenta só porque sabe usá-la — você usa porque ela é necessária e eficiente.

System Design abriu minha mente sobre quais ferramentas preciso aprender e tirou um peso dos meus ombros. Antes de entender isso, eu achava que precisava saber Kubernetes, Terraform e todas essas stacks para ser DevOps/Platform Engineer. Mas não — eu preciso resolver um problema com qualquer ferramenta que resolva a infraestrutura interna. Sei que as principais ferramentas para isso hoje são Kubernetes e Terraform, mas o conceito é o que é crucial. Agora eu entendo: "Não estude uma ferramenta, estude o conceito." Cache, filas e centenas de outros conceitos.
