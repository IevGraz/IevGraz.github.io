---
title: 'Kubernetes: Up and Running'
author:  Kelsey Hightower, Brendan Burns, Joe Beda, Lachlan Evenson
rating: 5
date: 2022-12-31
goodreads_link: https://www.goodreads.com/book/show/60888727-kubernetes
---

**Why I read this book:** I’ll be transitioning to the Platform backend team in a few months. I want to spend the time while I wait to learn something that could potentially ease my onboarding. 

**How I read this book:** I read the physical book. The chapters in the book are rather small and easy to comprehend. I read through a full chapter, highlighted the parts that seemed most interesting or useful and later wrote them all down. Once I’ve gone through the entire book, I re-read the notes to refresh my memory.

**What I liked about it:**

There were 3 attempts to teach me about Kubernetes in the past: a fellow backend engineer doing a learning session with a demo for our team; one of our SREs doing an extensive 4-hour workshop on Kubernetes basics; another SRE doing a short walk-through on our GitOps setup. None of these worked well for me. They jumped into the tooling without giving much context about the concepts used. I couldn't get over the fact that I don't understand why a Pod is called a Pod and therefore couldn't focus. This book, on the other hand, was the perfect level of abstraction to provide a context that I later could use when googling for how to do something specific. Oh, and also a Pod is a group of whales (so the naming goes with the whale theme of Docker containers).

As the book is written by the co-founders of the Kubernetes open source project, it has some sneak peeks into the philosophy of Kubernetes design, such as:

* **Coming in the front door** (an example of this would be replica sets using the same api we would to create a Pod manually)
* **Decoupling** (e.g. because Pods are not coupled to ReplicaSets and DaemonSets, every tool used for introspecting Pods in the context of ReplicaSets is equally applicable to Pods created by DaemonSets)

I found this rather exciting, as Kubernetes is a revolutionary technology that has had a major impact on the way software is built in the past decade.

I really liked how the information is structured. The concepts are introduced in a logical progression, with each concept building on the understanding gained from the previous one. For example, first introducing Pods, then ReplicaSets then Deployments. I feel like I really have a good mental model of the main concepts in Kubernetes and how they relate with each other after reading this book.

I’m also happy they are still keeping the book up to date. The third edition that I read was released only in August this year, so I wasn’t worried that I’m reading about outdated things.

**What I disliked:**

This wasn’t a problem for me, but I could imagine someone getting disappointed about this. The book is introductory level, reading it won’t make you an expert in Kubernetes, only familiar with it.

There were some chapters (mainly “Service discovery”) where I had to check the documentation to understand what the authors are trying to say better

There were very few illustrations. As a visual person I would appreciate the summary of some concepts as diagrams. For example the relationship between Kubernetes clusters and nodes vs Pods, ReplicaSets and Deployments. Here is my attempt to do it:

![Summary](/assets/images/kubernetes.drawio.svg){: width="600" }

