---
title: Database Reliability Engineering
subtitle: Designing and operating resilient database systems
author:  Laine Campbell, Charity Majors
rating: 3
date: 2022-08-17
goodreads_link: https://www.goodreads.com/book/show/36523657-database-reliability-engineering
---

**Why I read it:** One of the few areas where I still feel rather insecure professionally is databases. So I’m always looking for ways to improve myself. Although I have to admit I bought this particular book because it is published by O’reilly and has the word ‘database’ in the title.

**What I liked about it:** This was probably the first engineering book I read that was written by women, one of whom even developed a technical career after leaving music and theater. I really like finding more women in engineering to look up to.

The book begins with Maslow's hierarchy of needs applied to databases.

![Database hierarchy of needs](/assets/images/database_hierarchy_of_needs.drawio.svg){: width="500" }

I think that was a really neat literary trick.

In most chapters there were suggestions for other books to read, to get more in depth into the topic. I bought two more books while reading this one:

* [Infrastructure as Code by Kief Morris](https://www.goodreads.com/book/show/26544394-infrastructure-as-code)
* [Systems Performance by Brendan Gregg](https://www.goodreads.com/book/show/18058001-systems-performance) (this one is a really big book, but I saw a  suggestions to only read the beginnings of each chapter to get familiarized with the topic and dig deep in specific chapters when you’re dealing with a related problem)

My favorite chapter was ‘Infrastructure management’, which gave a brief overview of tools used for defining infrastructure as code. It was very interesting because the tools mentioned were the same as our SREs use at work. I used to know only the names of the tools but not what they do and why and this book changed that. 

There were also good (and very practical) chapters about Service Level Objectives (SLOs) and monitoring. They not only explained SLOs, but gave very concrete examples on how to define them. As well as a breakdown on why you need to be careful when averaging your monitoring data. I liked this part so much that I hope to write a short blog post based on it. 

Overall this book gives a good overview on how a mature (at least from technological perspective) organization operates. From things like infrastructure management, release management, observability to documentation and knowledge sharing (at least to some extent).

It is also  a good resource for someone who wants to get an overview on what kind of things an SRE job entails (the title says it is database specific, but that’s mostly the second half of the book). And that was kind of an interesting coincidence. I’m a senior software engineer and sometimes I start to think about what my next career chapter should be. One option is a broader, more abstract role of Software Architect (which I read about in [Fundamentals of Software Architecture](/book_reviews/fundamentals_of_software_architecture.html))). The other is going for technical depth instead of breadth. That could look like moving to a platform/ dev-tools kind of team and maybe later even a SRE team. So it was kind of cool that I got to read about both of these roles without really planning for it (as I bought this book on a whim).

**What I disliked:** The content of the book was very broad and very superficial. On the topics I already knew something about I didn’t really learn anything new. And on the topics I wasn’t really familiar with, I didn’t learn anything as there weren’t any explanations, only an assumption of prior knowledge. The main scenarios where I imagine this book being useful are:
* When you are new to the field of software engineering and want to get a broader perspective on how such organizations are run
* When  you need to dust off your general knowledge before a job interview
* When you are preparing some introductory level presentation on databases

My main goal when picking up this book was to improve my database knowledge. Unfortunately the book didn’t do anything for it, mainly for the reason described in the above paragraph.
The authors suggested very heavy testing in some scenarios e.g.
* Rule based validation that SQL is formatted correctly, number of rows potentially affected, etc. 
* Security tests as part of an automated test suite to check that vulnerabilities like opportunity for SQL injection are not being introduced.
* Downstream tests to ensure that any data pipeline is not adversely affected by the changes applied.

 I wonder how many organizations actually do something similar.

**Quote:**
_The goal of eliminating all risks is actually a poor one. Systems without stressors do not tend to strengthen and improve over time. They end up being brittle against unknown stressors. Systems that experience stressors regularly, and thus have been designed for resiliency, will tend to handle unknown risks more gracefully_ (I think this one applies to humans and our comfort zone as well).
