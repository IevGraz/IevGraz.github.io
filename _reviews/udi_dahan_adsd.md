---
title: Advanced Distributed Systems Design course
author: Udi Dahan
date: 2021-04-15
website: https://learn.particular.net/courses/adsd-online
---

I had quite a long  relationship with this course. My first attempt to watch it was with the Payments team in MobilePay. We used to dedicate an hour or two a week for learning. And one way to do it was by watching this course and discussing it. I don't remember why, but we stopped watching it at around 50% mark. Then global pandemic hit and Particular Software made the course free for people who want to spend their lock-down time learning about software architecture. I was one of those people but somehow my enthusiasm faded after re-watching the first 30%. I have moved on to a new job by then, but my colleagues at Vinted were also interested in the course and we decided to spend our learning budgets on buying a group access to it. Third time was actually a charm and I finally watched the entire course in a few months period. And want to share my impression of it.

### Contents of the course
- Explaining all the ways how network is unstable (fallacies of distributed computing)
- Explaining coupling and its effects on the system
- Introducing messaging and its benefits (as well as some important implementation details like handling messages that come out of order)
- Explaining the idea of Service Oriented Architecture (SOA)
- Explaining some concepts that will be helpful when building SOA
    - CQRS
    - Sagas (long-running processes)
- Few practical assignments to get the feel for SOA (services modelling for a hotel, saga design for loyal customers reward)
- Guiding through organizational changes and processes needed to introduce SOA

It also had few interesting detours
- Talking about dealing with business stakeholders and getting the real requirements/ problem to be solved
- Sharing some software industry history
- Sharing some common issues with caching and network performance optimization tips

### How I understood it

The course starts by explaining how network instabilities and coupling are bad for the performance of software systems. And since those things are bad 
we need to architecture our systems to minimize them. One approach to it is SOA. The main idea is to split the system into services in such a way that:
- Each service is autonomous (able to do everything it needs without the help of other services)
- Each service has explicit boundaries
- Each service is a technical authority for a business capability (an organization usually has few main business capabilities (maximum 7-10), so that's how many services there should be)
- To be able to fully fullfil the business capability service spans multiple technologies (backend, mobile, etc.) and therefore requires a cross-functional team to support it. 

Though there is a caveat to this seemingly strict division - SOA also includes 2 *bucket* services:
- IT/OPS that handles dependencies with 3rd parties (e.g. calling a Payment Service Provider API to actually charge user's card)
- Branding service that makes sure the UI is consistent (each service owns client side code to populate required data, but not how it is displayed on the screen).

In order to design such services we should move away from the common ways of thinking in entities and objects and building services around them. In the design phase we should avoid naming things (use shapes or colors for marking services instead) and just look for data that clumps together or the requirements that change together (or never change together). This way we should reach a stable division of responsibilities where the 'entities' are distributed between the services. 

Since services are autonomous, they shouldn't talk with each other much. And when communication is needed, it should happen via messaging instead of synchronous, blocking request-response calls. One case for such communication is a business process that spans multiple services. Each service should know its responsibility and cue on which logic should be executed. But no one should be responsible for the process orchestration - there shouldn't be any hierarchy between the services. One service simply executes its part of the logic and publishes an event, another service that cares about the event subscribes to it and does its part of the job when the event arrives. The events contain some sort of identifier (e.g. order id) that binds the entire process together.

### What I think about it
I think most software engineers would like to be able to find clear boundaries in the system, that require little communication over the network and supports new requirements easily and only by changing the internals of a single service. But the suggested method is rather hard to wrap your head around and apply in practice as both the concepts of avoiding entities and not having a single orchestrator are unusual and even opposite to the common ways of doing things. 

Plus the existence of two bucket services makes me a little suspicious. As most of the SOA seems to be about very strict division of responsibilities, and then suddenly you need 2 other services to do everything else. Though Udi Dahan argued that it is not exactly *everything else* but strict responsibilities of third party integration and branding. But my used-to-think-in-entities mind find it strange to imagine a single service integrating to both shipment and payment providers APIs.