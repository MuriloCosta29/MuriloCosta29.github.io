---
title: "Por que construí meu próprio GTD App"
date: 2026-03-18
translationKey: why-i-built-my-own-gtd-app
description: "Por que construí minha própria caixa de entrada GTD em Python — uma REST API sem distrações, feita para a forma como meu cérebro captura tarefas."
tags:
  - fastapi
  - python
  - docker
---

Eu usava o Notion para gerenciar tarefas, mas toda vez que abria o app para capturar uma ideia rápida, acabava me distraindo com o resto da tela. Eu precisava de uma caixa de entrada mais simples.

<!--more-->

## O problema com o Notion

O Notion é poderoso, mas esse era exatamente o problema para uma ferramenta de captura rápida. Eu queria abrir um app, escrever uma tarefa e fechar. Em vez disso, eu era puxado para bases de dados, páginas e templates toda vez que abria o Notion para adicionar um único item.

## A decisão de construir

Quando decidi construir minha própria caixa de entrada, eu estava nervoso — nunca tinha feito algo assim em Python, só em JavaScript. Mas a motivação era forte: eu queria uma ferramenta moldada ao jeito que meu cérebro funciona, não o contrário.

## O que o GTD App faz

A aplicação é simples, mas funciona. É uma REST API onde posso fazer capturas rápidas sem distração. Sem ruído de frontend, sem funcionalidades desnecessárias. Só uma caixa de entrada que faz uma coisa bem feita.

## O que aprendi construindo

Esse projeto me colocou em contato com várias tecnologias que eu queria aprender:

- **FastAPI** — Minha primeira vez trabalhando com uma REST API. A página automática `/docs` foi uma descoberta enorme.
- **SQLite + SQLAlchemy** — SQLite como banco de dados, SQLAlchemy como tradutor entre Python e SQL.
- **Docker** — Uso básico, mas a satisfação de containerizar um projeto real valeu a pena.

Esse foi o projeto que me fez perceber que quero continuar construindo ferramentas para resolver meus próprios problemas. O próximo é maior: [Deploy Tracker](/pt/blog/deploy-tracker-what-im-building-and-why/), um sistema de monitoramento com vários serviços.
