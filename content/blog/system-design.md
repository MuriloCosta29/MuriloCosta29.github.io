---
title: "What I Learned About System Design Building Deploy Tracker"
date: 2026-06-18
translationKey: deploy-tracker-system-design
description: "What building Deploy Tracker taught me about System Design: why there's no best stack, only the right context, and why trade-off is the keyword behind every architectural choice."
tags:
  - deploy-tracker
  - devops
  - system-design
---

When I finished Deploy Tracker, it worked — but I couldn't explain why I had chosen each tool. Redis or RabbitMQ? Celery or ARQ? I had answers, but not reasons. That gap had a name I didn't know yet: System Design.

<!--more-->

## How I Got Into System Design

System Design didn't come to my mind randomly. I watch videos from [Augusto Galego](https://www.youtube.com/watch?v=EWzVZA_qTEw), a CTO of a company outside Brazil and a sharp programmer. (If you want to watch the video and check out his channel, click his name.)

It started when I was scrolling through my YouTube timeline and found one of his videos talking about System Design. Modesty aside, I'm someone who wants to be the best programmer I can be — so I looked into it. But I realized it wasn't the right time to study this subject yet, and Augusto said something similar in the video.

So I left it for later. Then I went to write the Deploy Tracker README, and when I got to the part explaining why I chose each tool, I couldn't actually explain the reason behind the choices. That bothered me. And out of nowhere, the typical moment hit:

"Oh — this is System Design."

After that, I started to research: if I had known System Design, how would I have applied it to Deploy Tracker?

## What I Learned About Tools

To build a project, the right tool doesn't exist; the right context does.

When I "chose" my tools for Deploy Tracker, I didn't really compare options. For example, for the message broker I used Redis, but I could also have used RabbitMQ.

The same happened with the async worker: I used Celery, but ARQ was also an option.

But here is the thing: even though I didn't choose these tools by design, using them taught me real concepts like caching, queues, and asynchronous workers.

##### A Mid-Build Realization

At some point in the project — I don't remember how — I came across RabbitMQ, and considered using it, because I saw it was the market standard, and probably it would be better for me.

To my surprise, I saw that Redis + ARQ is the "best duo".

- "best duo" in quotes because → the best stack doesn't exist. A better context exists.

So I weighed the options:

For the message broker:

| Redis | RabbitMQ |
| :--- | :---: |
| Lightweight | Feature-rich |
| Simpler case | Complex case |

For the asynchronous worker:

| Celery | ARQ |
| :--- | :---: |
| Market standard | Not market standard |
| More setup to integrate with Redis | Built on Redis, simpler integration |

After weighing this, I decided I would use Redis because it fits a simpler case (which is my situation), and I'll also learn caching, which is the point.

For the asynchronous worker, Celery is the market standard, and that is enough for me.

To conclude, I understand the choice of this architecture, and for my case it really is the best.

## The Three Levels

I called this section "The Three Levels" because of: Junior, Mid-level, and Senior.

When I started studying System Design for this project, I asked an AI about how System Design applied to it, and it brought up these levels. I found it really interesting — so here is my current understanding, as a junior. I haven't lived the mid and senior levels yet, so take the next part as how I imagine it works, not as a fact.

**Junior / Intern.** For someone starting out, this full stack is the best option, because it forces you to study caching, background tasks, and queues. You finish the project with more tools and knowledge for your career. That was my case.

**Mid-level.** A mid-level dev probably already knows these concepts and wants to apply them — sometimes even over-engineering. But if they are mature, I imagine they would try to reduce the number of tools to keep things simpler. (I honestly don't know yet exactly which tools a mid-level would cut — this is just my guess.)

**Senior.** A senior probably wants the least operational stress possible 😂, and would use the minimum tools necessary. In Deploy Tracker, I imagine a senior might use FastAPI's BackgroundTasks instead of Celery, and for the database, something like AWS RDS (Relational Database Service) — which I discovered recently and found interesting, because it supports PostgreSQL, MySQL, and others.

## Trade-off

One more time, quoting [Galego](https://www.youtube.com/@GutoGalego) — I learned this word from him.

When I heard this word, I went to research its meaning. In the beginning, to be honest, I didn't understand it, but once I did, it seemed to fit into everything — and in System Design even more.

If you search for the definition of System Design on Google, you get this:

> "the process of defining the architecture, components, data flows, and interfaces of a software system to meet specific functional and business requirements."

That's why it screams TRADE-OFF. If you want to define architecture, components, data flows, and interfaces to achieve the most efficient project possible, you have to choose one thing and discard another — like "Redis or RabbitMQ?", "Celery or ARQ?", or "discard both and just use FastAPI's BackgroundTasks with AWS RDS". This is pure trade-off. You are giving up extra features you don't actually need, in exchange for more simplicity, stability, and efficiency.

## What Changes for Me Now

For me, System Design has the power to make you understand the code more deeply — the architecture, and what happens under the hood.

I like how this connects to my idea of understanding the code "completely".

- Completely = understanding the flow of the code.

As I said in my last post, I built Deploy Tracker too fast — and too fast meant I made it work without understanding the project completely.

This makes me invest more in the fundamentals of programming: C, pointers, memory, data structures, and more base. System Design showed me one cool truth: if you are at the beginning of your journey in programming, don't collect tools. In the future, you'll only use a tool if it's really necessary. You don't use a tool just because you know it — you use it because it's necessary and efficient.

System Design opened my mind about which tools I have to learn, and took a weight off my shoulders. Before understanding this, I thought I needed to know Kubernetes, Terraform, and all these stacks to be a DevOps/Platform Engineer. But no — I need to solve a problem with whatever tool solves the internal infrastructure. I know the main tools for this right now are Kubernetes and Terraform, but the concept is what's crucial. Now I understand: "Don't study a tool, study the concept." Caching, queues, and hundreds of other concepts.
