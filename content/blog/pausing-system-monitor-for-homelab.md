---
title: "Why I'm Pausing System Monitor To Build A Homelab"
date: 2026-09-06
translationKey: pausing-system-monitor-for-homelab
description: "Why I decided to pause my System Monitor project and focus on building a real homelab to learn DevOps and Platform Engineering from the ground up."
tags:
  - homelab
  - devops
  - platform-engineering
  - linux
  - networking
  - learning
---

I am pausing my System Monitor project.

Not because it is useless. Not because I lost interest. I am pausing it because I realized that, for the kind of engineer I want to become, I need a stronger foundation than another isolated application can give me.

<!--more-->

## The honest problem

System Monitor would teach me useful things: processes, files, permissions, resource usage, and networking. The idea was to build something close to `htop`, but with my own learning path around it.

But having a real Ubuntu Server changed the question.

Instead of building only another isolated application, I realized I had a playground to learn the infrastructure side more directly. If my goal is to become a DevOps or Platform Engineer, then I need to spend more time with the environment where software actually runs.

So I asked an AI a more direct question:

```text
What project can take me from the foundations to the kind of tools DevOps and Platform Engineers use in the market?
```

I mentioned that I had an Ubuntu Server, and that expanded the range of possible projects. That is where the homelab idea was born.

## Why a homelab

The new project is called **Homelab Platform**.

The homelab was the project idea the AI suggested after I said I wanted a project that started from the base and could grow toward the tools DevOps and Platform Engineers use in the market.

I had already seen homelabs in some YouTube videos, but I had never tried to build one myself. Now I want to try it on my humble desktop.

The idea is simple: turn that machine into a small production-like environment where I can deploy applications, configure services, break things, debug them, document the process, and later automate the setup.

What caught my attention is that a homelab would force me to learn things by hand first.

That matters because doing things by hand makes me see the real pieces:

- what the operating system is doing
- how the network is configured
- why SSH works or fails
- where logs live
- what a service needs to stay running
- what should be automated later

I do not want to start with automation before understanding what I am automating.

## Why not continue both projects

The honest answer is focus.

I am a Computer Science student. I do not have infinite time, and pretending that I can seriously build everything at once would be dishonest.

System Monitor is interesting, but the homelab is more aligned with my current goal.

When I asked for a project, the AI suggested a path that made sense to me because it starts from the beginning of DevOps work and slowly moves toward tools used in the industry today:

1. Apply Linux basics on a real server.
2. Configure the network.
3. Secure SSH access.
4. Set up a firewall.
5. Install Nginx.
6. Deploy a real application.
7. Add Docker Compose.
8. Add CI/CD.
9. Add monitoring.
10. Add backups.
11. Automate the server with Ansible.
12. Later, move into Kubernetes with k3s.

I already have some basic Linux knowledge from the Linux Essentials course by LinuxTips, but this project gives me a place to apply it for real. This sequence builds from fundamentals to DevOps and platform engineering, instead of jumping straight into advanced tools without context.

That connects with something I wrote in my previous post, [What I Learned About System Design Building Deploy Tracker](/blog/system-design/): I do not want to collect tools just because they are popular. I want to understand the concepts that make those tools necessary.

That is more valuable to me right now than finishing another standalone project.

## Learning With AI Without Skipping The Work

This matters because AI shaped the direction of the project. The answer was not to jump straight into Kubernetes or implement tools used in the industry before understanding the basics.

I liked that because it was brutally practical. A lot of DevOps content online starts too late in the story. It shows Kubernetes, Terraform, Argo CD, Vault, service mesh, and cloud architecture before the person truly understands Linux, networking, DNS, logs, ports, and deployments.

I will be honest: I still do not fully understand tools like service mesh, Argo CD, or Vault. I only started seeing these names while reading about what DevOps and Platform Engineers use in real jobs.

That is exactly why I do not want to start with them.

I decided to treat AI like a small technical organization around me:

- as a product manager only after I try to understand the project scope and create the issues myself
- as a senior engineer, challenging my decisions and explaining tradeoffs
- as a documentation assistant, helping me organize my notes

This is not a perfect simulation of a real company, obviously. But it gives me a structure: I can be the intern who tries to understand the work first, while the AI helps when I get stuck with scope, architecture, implementation, or documentation.

I still do not have perfect rules for AI usage. For now, I want to use common sense and create better rules from real experience.

That is probably a future blog post by itself, because it is hard to know when AI is helping and when it is replacing the part I should be doing myself. That is especially true as a student.

## How I want to learn

Honestly, I am afraid of using AI in a way that makes it do the work for me. But I think this fear is useful because it makes me more careful about how I use it.

This project has many topics I do not understand yet. Networking, SSH, gateways, subnets, DNS, Netplan, firewalls, and many other things are still new to me. But that is exactly why this project is useful. In the real world, especially in tech, we constantly face tools and problems we do not fully understand yet.

The important part is not confusing "making it work" with learning. I already wrote about this in the Deploy Tracker post: I built it too fast, and too fast meant I made things work before understanding them deeply.

I do not want to repeat that mistake here.

When an AI gives me a word I do not know, or when I need some concept before continuing a task, I should stop and fill that gap first. If my current knowledge is not enough to do the work, the next step is not to ask for the final answer. The next step is to learn the missing layer.

A simple example is Docker. I am studying Docker now, and it would not make sense to write a Dockerfile without understanding what an image, a container, and layers are.

Some knowledge layers need to be filled before starting an issue or changing a configuration file.

A good example happened when I was trying to connect to my Ubuntu Server through SSH. My Mac and my server were not using the same network gateway, and I had to understand what was happening before changing the Netplan YAML file in `/etc/netplan/`.

That was not originally a homelab task. It was just a casual problem from my day-to-day use of the server.

At that moment, the AI started mentioning many words I had never really understood before: gateway, subnet, DNS, static IP, DHCP, Netplan, routes, and `/24`.

My first reaction was confusion. But that confusion became useful because I had to stop and search for each concept. I had to connect the pieces instead of just asking for the final answer.

That simple SSH problem created a chain of questions:

- What is DHCP?
- What is Netplan?
- What is a gateway?
- What is a subnet?
- Why did my Mac and Ubuntu Server end up in different networks?
- When should I use a static IP?
- When is DHCP reservation better?
- What does DNS actually affect?

This is the line I do not want to cross:

```text
Here is my gateway, here is my Mac IP, here is my YAML file. Rewrite the Netplan config for me.
```

If I did only that, maybe SSH would work. But I would not understand why it worked.

For example, I would miss things like:

- why `192.168.x.x` is commonly used in private home networks
- why my Mac and server need to be in the same subnet
- what `192.168.0.x` means in my local network
- what `/24` means
- why `.0` and `.255` usually have special meanings in a common `/24` network
- why `.1` is often used by the router
- why the last number of the IP should be chosen carefully
- what DNS affects and what it does not affect

I also realized that some things I thought I knew were not that solid. For example, I had this idea that `.1` and `.254` were always reserved, but that is not exactly true. In a common `/24` network, `.0` usually represents the network address, `.255` is usually the broadcast address, and `.1` is often used by the router by convention.

So yes, I had to slow down. My brain wanted to skip to "just make SSH work", but the whole point of this project is not letting that happen.

I am realizing that knowledge usually comes with time, friction, and some pain. If AI removes all of that, it also removes part of the learning.

So my goal is to use AI carefully. I want to use it to explain, challenge, review, and guide me, but not to replace the work I need to do myself.

I do not want to vibe code and pretend I am learning.

The pain of learning is necessary.

## The next step

The next step is to organize the project like real work.

I want to define the scope, create issues, understand what I need to learn before each task, and document the decisions. The first practical task is still simple: make the server network stable and connect through SSH without depending on a monitor.

That is not glamorous, but it is the foundation.
