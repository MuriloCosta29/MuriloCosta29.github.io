---
title: "Why I Built My Own GTD App"
date: 2026-03-18
tags:
  - FastAPI
  - Python
  - Docker
---

I was using Notion for task management, but every time I opened it to capture a quick thought, I got distracted by everything else on the screen. I needed a simpler inbox.

<!--more-->

## The problem with Notion

Notion is powerful, but that's exactly the problem for a quick capture tool. I wanted to open an app, type a task, and close it. Instead, I was being pulled into databases, pages, and templates every time I opened Notion to add a single item.

## The decision to build

When I decided to build my own inbox, I was nervous — I had never built anything like this in Python, only in JavaScript. But the motivation was strong: I wanted a tool shaped around how my brain works, not the other way around.

## What the GTD App does

The application is simple but effective. It's a REST API where I can do fast captures with zero distractions. No frontend noise, no unnecessary features. Just an inbox that does one thing well.

## What I learned building it

This project introduced me to several technologies I had always wanted to learn:

- **FastAPI** — My first time working with a REST API. The automatic `/docs` page was a revelation.
- **SQLite + SQLAlchemy** — SQLite as the database, SQLAlchemy as the translator between Python and SQL.
- **Docker** — Basic usage, but the satisfaction of containerizing a real project was worth it.

This was the project that made me realize I want to keep building tools that solve my own problems. The next one is bigger: [Deploy Tracker](/blog/deploy-tracker), a multi-service monitoring system.
