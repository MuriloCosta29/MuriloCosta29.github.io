---
title: "I Built Deploy Tracker Too Fast"
date: 2026-05-31
translationKey: deploy-tracker-too-fast
description: "What Deploy Tracker taught me about moving too fast, stacking tools before fundamentals, and going back to Linux, networking, and systems foundations."
tags:
  - deploy-tracker
  - devops
  - linux
  - networking
  - observability
  - docker
---

Deploy Tracker was not a failure. It was a mirror. It showed me that I could build something bigger than a CRUD, but it also showed me that I was stacking tools before training the foundations behind them.

<!--more-->

## What Deploy Tracker was supposed to be

Deploy Tracker was supposed to be a deployment monitoring dashboard with observability.

The idea was simple: register applications, monitor their health, collect metrics, display status, show logs, and trigger alerts when downtime happens.

Repository: [Deploy Tracker](https://github.com/MuriloCosta29/deploy-tracker)

When I started Deploy Tracker, I had two main goals:

1. Move away from basic CRUD projects.
2. Get closer to the tools used in the DevOps world.

That is why I chose technologies like FastAPI, PostgreSQL, Redis, Celery, Prometheus, Grafana, Docker Compose, GitHub Actions, and Nginx.

At the time, it felt like the right next step.

And in some ways, it was.

## What I got right

Two important things.

1. I learned a lot from this project, and I do not regret building it. Because of Deploy Tracker, I found problems that could have appeared much later in my journey, even if some of them were basic.
2. I know that in programming, I will never know everything. So I should not let one small unknown stop me from finishing a project. In this case, the problem was different: I realized that what I did not know was not just a small detail. It was part of the foundation. And a strong foundation is crucial.

The real problem was not FastAPI, Redis, Celery, Docker, Prometheus, or Grafana.

The problem was that I was using tools built on top of foundations I had not trained enough yet.

Because I did not understand HTTP deeply enough, FastAPI felt easier than it really was.

- I could create routes, but I could not fully explain what happened between a client sending a request and the API returning a response.
- I could read Swagger, but I did not deeply understand headers, status codes, request bodies, query parameters, and path parameters.

Because I did not understand networking deeply enough, Docker Compose and Nginx hid important details from me.

- I could run multiple containers, but I did not fully understand how they communicated.
- I used ports, service names, and `localhost`, but I did not understand the difference between `localhost` on my machine and `localhost` inside a container.
- I added Nginx as a reverse proxy, but I did not fully understand what was happening when a request was forwarded to the API.

Because I did not understand Linux processes and services deeply enough, Celery felt like magic.

- I could run a worker and a beat scheduler, but I did not fully understand what a worker process was doing.
- I used background jobs, but I needed a better understanding of processes, signals, services, and failure handling.
- The hardcoded health check problem showed me that I was making the system run without fully thinking through how the workflow should behave.

Because I did not understand caching deeply enough, Redis became just another tool in the stack.

- I knew Redis could make reads faster, but I needed to understand cache invalidation, TTL, stale data, and what should happen when Redis is unavailable.
- I used Redis, but I did not fully understand the operational problems that come with caching.

Because I did not understand observability deeply enough, Prometheus and Grafana became more about dashboards than diagnosis.

- I exposed metrics and created a Grafana dashboard, but I still needed to understand what makes a metric useful.
- I needed to understand the difference between logs, metrics, traces, dashboards, and alerts.
- I could see graphs, but I was not yet ready to design observability from first principles.

Because I did not understand configuration and deployment deeply enough, some parts of the project were too tied to my local environment.

- I used hardcoded values where configuration should have been explicit.
- I did not separate local development settings from production-like settings well enough.
- I needed to understand why `.env.example`, secrets, environment variables, and service configuration matter.

The biggest lesson is this:

I could make the system run, but I could not explain every important layer that made it work.

## The mistake

The mistake was not building Deploy Tracker.

The mistake was building it too fast.

I stacked advanced tools before training the foundations that those tools depend on. I was learning how to connect services together, but I was not always understanding the layers underneath them.

That is dangerous, especially for someone who wants to become a DevOps or Platform Engineer.

In backend development, it is already important to understand the foundations. In DevOps and Platform Engineering, it is even more important, because the job is not only to write code. The job is to understand systems, failures, deployment environments, networks, services, logs, metrics, reliability, and infrastructure.

If I do not understand the foundation, I can still copy commands, run containers, expose dashboards, and make a project look impressive.

But when something breaks, I will not know where to look first.

That was the real problem.

## When I noticed it

I started noticing the problem while working with FastAPI.

At first, creating endpoints felt simple. I could define a route, open Swagger, send a request, and get a response.

But then I saw HTTP methods like `GET`, `POST`, `PATCH`, and `DELETE`, and I caught myself thinking:

> What exactly is an HTTP method?

That question bothered me.

Not because asking it was bad, but because it showed me that I was using a web framework before understanding enough about the protocol behind it.

I could write:

```python
@router.get("/applications")
```

But I could not fully explain what happened from the moment a client sent that request to the moment FastAPI returned a response.

Then the same pattern started appearing in other parts of the project.

I could run containers with Docker Compose, but I did not deeply understand container networking.

I could add Nginx, but I did not fully understand reverse proxy behavior inside a Docker network.

I could run Celery, but I did not deeply understand workers, queues, process behavior, retries, and failure handling.

I could expose Prometheus metrics and build a Grafana dashboard, but I was still learning the difference between real observability and just having graphs on a screen.

The project worked.

But working is not the same thing as understanding.

## Why this matters

For a long time, I thought that getting closer to DevOps meant using more DevOps tools.

- Docker.
- Redis.
- Celery.
- Prometheus.
- Grafana.
- Nginx.
- CI/CD.

Those tools matter, but they are not the foundation.

The foundation is understanding what happens underneath:

- How HTTP works.
- How processes run.
- How services communicate.
- How ports and sockets work.
- How Linux represents system information.
- How logs are produced and consumed.
- How metrics describe system behavior.
- How background jobs fail.
- How configuration enters an application.
- How deployment environments differ from local development.

DevOps and Platform Engineering are not about collecting tools on a resume.

They are about understanding systems well enough to build, run, debug, and improve them.

Deploy Tracker taught me that I was trying to climb too high without checking if the base was strong enough.

## How I am fixing it

To fix this, I created another project: System Monitor.

System Monitor is a Linux system monitoring tool written in C.

The goal is not to use advanced tools. The goal is to understand the operating system better by reading information directly from Linux interfaces like `/proc`, `/etc/passwd`, `/var/log`, and system calls.

With this project, I want to study:

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
- Terminal UI with `ncurses`

This is not as shiny as a dashboard with Prometheus and Grafana.

But it is closer to the foundation I need.

If I want to become a DevOps or Platform Engineer, I need to understand Linux, networking, services, and system behavior. Not just the tools built on top of them.

## What happens next

I am not abandoning Deploy Tracker.

I am stepping back so I can return to it with more maturity.

After I build a stronger foundation with System Monitor, I want to go back to Deploy Tracker and rebuild parts of it with a deeper understanding of the systems behind it.

Some things I want to revisit:

- The health check workflow.
- The Celery scheduler.
- Docker Compose networking.
- Nginx reverse proxy configuration.
- Environment-based configuration.
- Tests for application and health check flows.
- CI/CD responsibilities.

I also want to write individual posts about the tools I used in Deploy Tracker:

- Celery
- Prometheus
- Grafana
- GitHub Actions
- CI/CD
- Docker Compose
- Nginx

But this time, I do not want to write only about how I used them.

I want to write about why they exist, what problem they solve, what foundation they depend on, and what I misunderstood when I first used them.

## Final thoughts

Deploy Tracker was not a failure.

It was a mirror.

It showed me that I can build projects, connect tools, and finish something bigger than a CRUD.

But it also showed me that ambition without foundation can make me move too fast in the wrong direction.

That is the real lesson.

I do not regret building Deploy Tracker.

I am glad I built it.

Because now I know what I need to fix.
