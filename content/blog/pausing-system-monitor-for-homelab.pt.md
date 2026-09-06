---
title: "Por que estou pausando o System Monitor para construir um Homelab"
date: 2026-09-06
translationKey: pausing-system-monitor-for-homelab
description: "Por que decidi pausar meu projeto System Monitor e focar em construir um homelab real para aprender DevOps e Platform Engineering desde a base."
tags:
  - homelab
  - devops
  - platform-engineering
  - linux
  - redes
  - aprendizado
---

Estou pausando meu projeto System Monitor.

Não porque ele é inútil. Não porque perdi o interesse. Estou pausando porque percebi que, para o tipo de engenheiro que quero me tornar, preciso de uma base mais forte do que outro projeto isolado pode me dar.

<!--more-->

## O problema honesto

System Monitor me ensinaria coisas úteis: processos, arquivos, permissões, uso de recursos e redes. A ideia era construir algo próximo ao `htop`, mas com meu próprio caminho de aprendizado em volta disso.

Mas ter um Ubuntu Server real mudou a pergunta.

Em vez de construir apenas mais uma aplicação isolada, percebi que eu tinha um playground para aprender o lado de infraestrutura de forma mais direta. Se meu objetivo é me tornar DevOps ou Platform Engineer, então preciso passar mais tempo no ambiente onde o software realmente roda.

Então fiz uma pergunta mais direta para uma IA:

```text
Qual projeto pode me levar dos fundamentos até o tipo de ferramenta que DevOps e Platform Engineers usam no mercado?
```

Eu mencionei que tinha um Ubuntu Server, e isso expandiu o leque de projetos possíveis. Foi aí que nasceu a ideia do homelab.

## Por que um homelab

O novo projeto se chama **Homelab Platform**.

O homelab foi a ideia de projeto que a IA sugeriu depois que eu disse que queria um projeto que começasse pela base e pudesse crescer em direção às ferramentas que DevOps e Platform Engineers usam no mercado.

Eu já tinha visto homelabs em alguns vídeos no YouTube, mas nunca tinha tentado construir um. Agora quero tentar fazer isso no meu humilde desktop.

A ideia é simples: transformar essa máquina em um pequeno ambiente parecido com produção, onde eu possa fazer deploy de aplicações, configurar serviços, quebrar coisas, debugar, documentar o processo e depois automatizar a configuração.

O que chamou minha atenção é que um homelab me forçaria a aprender as coisas na unha primeiro.

Isso importa porque fazer as coisas na mão me faz enxergar as peças reais:

- o que o sistema operacional está fazendo
- como a rede está configurada
- por que SSH funciona ou falha
- onde os logs ficam
- o que um serviço precisa para continuar rodando
- o que deve ser automatizado depois

Eu não quero começar com automação antes de entender o que estou automatizando.

## Por que não continuar os dois projetos

A resposta honesta é foco.

Sou estudante de Ciência da Computação. Eu não tenho tempo infinito, e fingir que consigo tocar tudo ao mesmo tempo com seriedade seria mentira.

System Monitor é interessante, mas o homelab está mais alinhado com meu objetivo atual.

Quando pedi um projeto, a IA sugeriu um caminho que fez sentido para mim porque começa no início do trabalho de DevOps e vai avançando aos poucos em direção a ferramentas usadas na indústria hoje:

1. Aplicar Linux básico em um servidor real.
2. Configurar a rede.
3. Proteger o acesso SSH.
4. Configurar firewall.
5. Instalar Nginx.
6. Fazer deploy de uma aplicação real.
7. Adicionar Docker Compose.
8. Adicionar CI/CD.
9. Adicionar monitoramento.
10. Adicionar backups.
11. Automatizar o servidor com Ansible.
12. Depois, entrar em Kubernetes com k3s.

Eu já tenho uma noção básica de Linux por causa do curso Linux Essentials da LinuxTips, mas esse projeto me dá um lugar para aplicar isso de verdade. Essa sequência constrói dos fundamentos até DevOps e Platform Engineering, em vez de pular direto para ferramentas avançadas sem contexto.

Isso se conecta com algo que escrevi no meu post anterior, [What I Learned About System Design Building Deploy Tracker](/blog/system-design/): eu não quero colecionar ferramentas só porque elas são populares. Quero entender os conceitos que fazem essas ferramentas serem necessárias.

Isso é mais valioso para mim agora do que finalizar mais um projeto separado.

## Aprendendo com IA sem pular o trabalho

Isso importa porque a IA moldou a direção do projeto. A resposta não foi pular direto para Kubernetes nem implementar ferramentas usadas na indústria antes de entender a base.

Gostei disso porque foi brutalmente prático. Muito conteúdo de DevOps na internet começa tarde demais na história. Mostra Kubernetes, Terraform, Argo CD, Vault, service mesh e arquitetura cloud antes da pessoa entender bem Linux, rede, DNS, logs, portas e deploys.

Vou ser honesto: ainda não entendo completamente ferramentas como service mesh, Argo CD ou Vault. Comecei a ver esses nomes lendo sobre o que DevOps e Platform Engineers usam em trabalhos reais.

É exatamente por isso que não quero começar por elas.

Decidi tratar IA como uma pequena organização técnica ao meu redor:

- como product manager, só depois de eu tentar entender o escopo do projeto e criar as issues sozinho
- como engenheiro sênior, questionando minhas decisões e explicando tradeoffs
- como assistente de documentação, me ajudando a organizar minhas anotações

Obviamente, isso não é uma simulação perfeita de uma empresa real. Mas me dá uma estrutura: eu posso ser o estagiário que tenta entender o trabalho primeiro, enquanto a IA ajuda quando eu travo em escopo, arquitetura, implementação ou documentação.

Ainda não tenho regras perfeitas para usar IA. Por enquanto, quero usar bom senso e criar regras melhores a partir da experiência real.

Isso provavelmente vira um post futuro, porque é difícil saber quando a IA está ajudando e quando está substituindo a parte que eu deveria fazer sozinho. Isso é especialmente verdade sendo estudante.

## Como quero aprender

Honestamente, tenho medo de usar IA de um jeito que faça ela trabalhar por mim. Mas acho que esse medo é útil, porque me deixa mais cuidadoso sobre como uso IA.

Esse projeto tem muitos assuntos que ainda não entendo. Redes, SSH, gateways, subnets, DNS, Netplan, firewalls e muitas outras coisas ainda são novas para mim. Mas é exatamente por isso que esse projeto é útil. No mundo real, principalmente em tecnologia, encontramos ferramentas e problemas que ainda não entendemos completamente o tempo todo.

O importante é não confundir "fazer funcionar" com aprender. Eu já escrevi sobre isso no post do Deploy Tracker: construí rápido demais, e rápido demais significou fazer as coisas funcionarem antes de entendê-las profundamente.

Não quero repetir esse erro aqui.

Quando uma IA me dá uma palavra que não conheço, ou quando preciso de algum conceito antes de continuar uma tarefa, eu devo parar e preencher essa lacuna primeiro. Se meu conhecimento atual não é suficiente para fazer o trabalho, o próximo passo não é pedir a resposta final. O próximo passo é aprender a camada que falta.

Um exemplo simples é Docker. Estou estudando Docker agora, e não faria sentido escrever um Dockerfile sem entender o que são imagem, container e layers.

Algumas camadas de conhecimento precisam ser preenchidas antes de começar uma issue ou alterar um arquivo de configuração.

Um bom exemplo aconteceu quando eu estava tentando conectar no meu Ubuntu Server via SSH. Meu Mac e meu servidor não estavam usando o mesmo gateway de rede, e eu precisei entender o que estava acontecendo antes de alterar o arquivo YAML do Netplan em `/etc/netplan/`.

Isso não era originalmente uma tarefa do homelab. Era só um problema casual do meu uso diário do servidor.

Naquele momento, a IA começou a mencionar várias palavras que eu nunca tinha entendido de verdade: gateway, subnet, DNS, IP fixo, DHCP, Netplan, routes e `/24`.

Minha primeira reação foi confusão. Mas essa confusão virou útil porque precisei parar e pesquisar cada conceito. Precisei conectar as peças em vez de apenas pedir a resposta final.

Esse problema simples de SSH criou uma cadeia de perguntas:

- O que é DHCP?
- O que é Netplan?
- O que é gateway?
- O que é subnet?
- Por que meu Mac e meu Ubuntu Server ficaram em redes diferentes?
- Quando devo usar IP fixo?
- Quando DHCP reservation é melhor?
- O que DNS realmente afeta?

Essa é a linha que eu não quero cruzar:

```text
Aqui está meu gateway, aqui está o IP do meu Mac, aqui está meu arquivo YAML. Reescreva a configuração do Netplan para mim.
```

Se eu fizesse só isso, talvez o SSH funcionasse. Mas eu não entenderia por que funcionou.

Por exemplo, eu perderia coisas como:

- por que `192.168.x.x` é comum em redes domésticas privadas
- por que meu Mac e meu servidor precisam estar na mesma subnet
- o que `192.168.0.x` significa na minha rede local
- o que `/24` significa
- por que `.0` e `.255` geralmente têm significados especiais em uma rede `/24`
- por que `.1` costuma ser usado pelo roteador
- por que o último número do IP precisa ser escolhido com cuidado
- o que DNS afeta e o que ele não afeta

Também percebi que algumas coisas que eu achava que sabia não eram tão sólidas. Por exemplo, eu tinha a ideia de que `.1` e `.254` eram sempre reservados, mas isso não é exatamente verdade. Em uma rede `/24`, `.0` geralmente representa o endereço da rede, `.255` geralmente é o endereço de broadcast, e `.1` costuma ser usado pelo roteador por convenção.

Então sim, precisei desacelerar. Meu cérebro queria pular para "só fazer o SSH funcionar", mas o ponto desse projeto é justamente não deixar isso acontecer.

Estou percebendo que conhecimento geralmente vem com tempo, atrito e um pouco de dor. Se a IA remove tudo isso, ela também remove parte do aprendizado.

Então meu objetivo é usar IA com cuidado. Quero usar para explicar, questionar, revisar e me guiar, mas não para substituir o trabalho que eu preciso fazer.

Eu não quero fazer vibe code e fingir que estou aprendendo.

A dor de aprender é necessária.

## O próximo passo

O próximo passo é organizar o projeto como trabalho real.

Quero definir o escopo, criar issues, entender o que preciso aprender antes de cada tarefa e documentar as decisões. A primeira tarefa prática ainda é simples: deixar a rede do servidor estável e conectar via SSH sem depender de um monitor.

Isso não é glamouroso, mas é a fundação.

