---
title: "Deploy Tracker -- por que e o que é"
date: 2026-03-28
translationKey: deploy-tracker-what-im-building-and-why
description: "A arquitetura, a stack e a mentalidade sem-tutorial por trás do Deploy Tracker — meu sistema assíncrono de health checks entre engenharia backend e DevOps."
tags:
  - fastapi
  - postgresql
  - redis
  - celery
  - docker-compose
  - prometheus
  - grafana
  - github-actions
  - nginx
---

Era hora de sair da zona de conforto dos CRUDs. Este post mostra a arquitetura, a stack e a mentalidade de "sem tutorial" por trás do meu novo sistema assíncrono de health checks.

<!--more-->

## Por que esse projeto

**O problema:** Meu GitHub estava cheio de aplicações CRUD simples.

**A busca:** Considerei projetos mais simples, mas queria um desafio real, algo que mostrasse pensamento de infraestrutura, não apenas endpoints básicos de API.

**A solução:** Escolhi o Deploy Tracker porque ele combina uma base backend sólida com cultura DevOps real.

Quando procurei o desafio certo para conectar Back-End Engineering e DevOps, meu mentor me apresentou três opções, e avaliamos cada uma juntos.

A primeira sugestão foi um **Pomodoro Timer**. Criar uma interface personalizada para acompanhar minhas próprias métricas parecia interessante, mas a stack seria praticamente igual à do meu último GTD App: FastAPI, SQLite e Docker.

A segunda foi um **URL Shortener**. Esse já era mais desafiador. A stack subiria de nível: FastAPI, PostgreSQL, Redis, Nginx, Docker Compose, GitHub Actions e testes automatizados.

Isso chegou perto do que eu queria, mas eu ainda queria explorar melhor a cultura DevOps. Olhei para a stack que estava montando:

**FastAPI & PostgreSQL:** Base sólida e gerenciamento de dados.

**Redis & Nginx:** Performance e gerenciamento de tráfego.

**Docker Compose:** Containerização e ambientes padronizados.

**GitHub Actions:** CI/CD.

Para capturar melhor a mentalidade DevOps, percebi que precisava de ferramentas de observabilidade. Depois de pesquisar, decidi não usar Kubernetes ainda — é complexo demais para o meu momento e provavelmente atrapalharia minha curva de aprendizado, porque ainda não tenho a base necessária. Em vez disso, escolhi **Prometheus e Grafana**.

Combinando essa stack com a necessidade de uma aplicação mais próxima do mundo real, a terceira sugestão do meu mentor foi a melhor escolha: o **Deploy Tracker**.

## O que ele faz

O **Deploy Tracker** é uma aplicação que registra e monitora deploys. Por exemplo: se eu fizer o deploy de uma aplicação minha, ele mostra **status**, **logs** e **alerta se algo cair**.

## A arquitetura

A arquitetura completa é:

**FastAPI** - Recebe webhooks de deploy e health checks.

**PostgreSQL** - Histórico de deploys, status e metadados.

**Redis** - Recebe tarefas da API e envia para o worker assíncrono.

**Celery** - Worker assíncrono. Executa os health checks enviados pelo Redis.

**Prometheus** - Coleta métricas como latência, uptime e status HTTP.

**Grafana** - Dashboard com métricas visuais.

**Docker Compose** - Seis containers orquestrados.

**GitHub Actions** - CI/CD com testes, builds e lint.

**Nginx** - Reverse proxy.

## Roteiro

**Semana 1:** FastAPI + PostgreSQL (core da API + banco de dados)

**Semana 2:** Redis (camada de cache)

**Semana 3:** Celery (workers assíncronos + health checks)

**Semana 4:** Prometheus (coleta de métricas)

**Semana 5:** Grafana (dashboards de monitoramento)

**Semana 6:** GitHub Actions (pipeline de CI/CD)

**Semana 7:** Nginx (reverse proxy) + Docker Compose (orquestração completa)

**Semana 8:** Polimento do README, testes e ajustes finais

**Ferramenta para organizar o projeto:** considerei usar Jira, já que usamos na faculdade, mas ele tinha recursos demais para um projeto solo. Escolhi GitHub Projects com um quadro Kanban.

**Curiosidade sobre projetos no GitHub:** se você escreve `closes <issue number>` no final de um commit, o GitHub fecha a issue automaticamente. Eu sei que é simples, mas achei legal.

![Task Dashboard](/images/dashboard-screenshot.png)

Meu dashboard no dia em que escrevi este post.

## Como estou construindo

O produto final é importante, mas meu foco real é o processo de engenharia por trás dele. Estou construindo o Deploy Tracker sem tutoriais passo a passo e sem copiar código. O ciclo é simples e rigoroso: ler documentação oficial, implementar, falhar e tentar de novo.

Essa imersão ficou tão forte que às vezes me pego sonhando com linhas de código. Ao passar pelos primeiros estágios do projeto e integrar ferramentas como Redis, percebi algo importante: forçar minha mente a escrever o código do zero muda minha perspectiva. Não é só fazer funcionar; é enxergar e entender a arquitetura de verdade.

**Regra #1**

Criei uma regra rígida para este projeto: nenhum código entra no repositório se eu não entender exatamente como e por que ele funciona. Essa abordagem mudou completamente a forma como resolvo problemas. Antes, eu só tinha ouvido falar de Stack Overflow de passagem; agora, junto com documentação oficial, ele virou uma ferramenta essencial para entender discussões técnicas e debugar erros reais.

**Regra #2**

Uma ferramenta, não uma muleta.

Uso IA ativamente, mas como mentor educacional. Uso para entender como ferramentas funcionam por baixo dos panos ou para esclarecer conceitos complexos, mas nunca para escrever o código por mim. O objetivo é construir uma base sólida, não pular a curva de aprendizado.
