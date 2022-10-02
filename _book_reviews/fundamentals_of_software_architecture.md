---
title: Fundamentals of Software Architecture
subtitle: An Engineering Approach
author:   Mark Richards, Neal Ford
rating: 3
date: 2022-02-26
goodreads_link: https://www.goodreads.com/book/show/44144493-fundamentals-of-software-architecture
---
__Why I read it:__ I overhear something about different architecture styles here and there, but never had a coherent picture. For example how the typical layered architecture contrast against the onion one? Does Domain Driven Design relate to any of those things in any way? I hoped this book could help me finally build that picture.

I discussed this book and why am I reading it with a colleague and he recommended to also watch a Youtube [video](https://www.youtube.com/watch?v=5OjqD-ow8GE) by Simon Brown on Modular Monoliths and read David Pereira's [blog series](https://pereiren.medium.com/clean-architecture-series-part-1-f34ef6b04b62) on clean architecture. 

So this review will discuss all these things.

__Short Summary:__ 
The book contains 3 parts:
- One explaining main concepts of Software Architecture like types of architecture characteristics, concepts like cohesion and coupling, etc;
- One discussing the actual architecture styles and how they result in different characteristics (rating them in 5 star scale);
- One diving into the social skills of the architect role and navigating the day-to-day tasks.

__What I liked about it:__ 
This was not something I came for to this book, but it gave me a better understanding of the role of software architect and the skills needed. I used to consider this as a path for myself because I seem to be better at abstract, high level thinking than optimizing technical details. But according to the book the architect's role is more about the breadth of technical knowledge - having at least little experience with many different things. Plus being able to form a long term vision and align it with various practicalities. So this no longer seems like a good role for me.

As for the things I came here for, I think I got them to some extent. I have an overview now of different architecture styles and how they result in different system properties. About Domain Driven Design - it seems _design_ is one step lower than _architecture_ - more about the classes and how they interact with each other. 

There were interesting practical things mentioned, like:
  - Architecture unit testing frameworks like [NetArchTest](https://github.com/BenMorris/NetArchTest), that, for example, allow to programmatically ensure correct dependencies between layers. 
  - Architecture [katas](https://nealford.com/katas/) as a way to practice in small groups.

I've learned about architecture styles I haven't heard before, like Microkernel and Space-based. Authors even discussed a lot of implementation practicalities, e.g. using replicated vs distributed caching for Space-based architecture and pros and cons of each approach. I think even if I won't remember the details, reading through these considerations helps to form some sort of (subconscious) understanding and my approach to software design.  

My favorite part by far was the pyramid of knowledge and how it relates with day-to-day work and career profile - balancing the portfolio of knowledge regarding depth vs. breadth.

![The pyramid of knowledge](/assets/images/fundamentals_software_architecture.drawio.svg){: width="375" }

- The _stuff you know_ is the stuff you use daily to perform your job; 
- The _stuff you don't know_ is the stuff you heard about but have little to no experience with;
- The _stuff you don't know you don't know_ is the stuff that would be the perfect solution to your problem, but you don't know it exists.

I also loved the quote 'The stuff you know is also the stuff you must maintain - nothing is static in software world'.

__What I disliked:__
Two-thirds of the book were more about the role of the architect rather than the architecture. So it was a much 'softer' book than I hoped it to be. 

I had a feeling that there was too much useless text in the book. Sentences were too long somehow, overstating the obvious. And the part about architecture styles had a lot of repetition. Each style had a chart of architecture characteristics ratings and a short explanation why they are like that. A lot of it could have been summarized into monolithic vs. distributed deployment, instead of being repeated with every style:
- __Monolithic:__ Low deployability ratings as even the smallest change requires redeploying the entire thing which often leads to low frequency deployments; low testability rating as there is too much testing to be done and people tend to skip it out of laziness; low fault tolerance as issue in one place will bring the entire system down; medium reliability as there is no network traffic within the system; high simplicity as you don't have to reason about distributed parts communicating with each other, etc.
- __Distributed:__ High deployability, testability and fault tolerance due to smaller independent units; high agility as it is easy to evolve and test the system; low performance if there are many network calls to be made (and each call has some authentication checks).

A lot of explanations in the book were somehow too abstract. Best example of this was the chapter on Event-driven architecture. The initial explanation contained terms like _initiating event_, _event channel_ and _event processor_ instead of terms like _publisher_, _queue_, _consumer_, _command_ and _event_ that are usually used to talk about this architecture style. The concepts of command vs. event were introduced later, but in a way that didn't help to understand full picture better. I found this a bit funny, as I thought of it as an example of what happens when architects architect for too long and get lost in the Abstraction land. 

However I managed to follow the book's content quite well. Mostly because I was already familiar with a lot of the concepts from other sources. For example Udi Dahan's [Advanced Distributed Systems Design course](/reviews/udi_dahan_adsd.html) where he also talks about (affrent and effrent) coupling, fallacies of distributed computing, bus vs. broker messaging styles, service oriented architecture and a lot more. And in a much more approachable way (maybe partly because it is a video + slides, so richer communication channels).

The book is best suited for enterprise architects. Not only because all the examples were either Java or .NET, but also a lot of the advice about navigating politics seemed like the things that happen in big organizations. 

__How the other resources relate to the book content?__ 

Simon Brown's video on Modular Monoliths gave a better explanation of Software Architecture as a way of packaging code (by layer, by feature, etc.). It talked a bit about Ports & Adapters architecture style and keeping domain related code separate from technical stuff, which wasn't mentioned in the book at all. David Pereira's blog series expanded on it a lot more - comparing Ports & Adapters to Onion to Clean architecture. Yet the blog was not as good on discussing the resulting architecture characteristics and why they are like that. So all in all it was a good combination to start with the book (establishing or strengthening the base vocabulary and understanding) and then move on to specific resources. 