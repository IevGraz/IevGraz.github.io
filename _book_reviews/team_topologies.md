---
title: 'Team Topologies: Organizing Business and Technology Teams for Fast Flow'
author:  Matthew Skelton, Manuel Pais
rating: 3
date: 2023-08-25
goodreads_link: https://www.goodreads.com/book/show/44135420-team-topologies
---

**Why I read this book:**  It seems to be popular among the managers in my current workplace. I was always curious what the people that organize the ways we work are inspired by. Plus a colleague read it recently and seemed quite hyped about it. 

**How I read this book:**  I bought a copy a while ago, but never got around to reading it. So I decided to listen to an audio version first and see if there is something valuable for me there. Indeed there was as the book talks a lot about platform and enabling teams. I’m currently a part of a platform team and wanted to explore in more detail how the authors define them. 

**What I liked about it:**


There were two topics that I was  most interested in:

<ins>Cognitive load on software development teams.</ins> The authors seem to consider cognitive load on a team the main issue that we need to tackle to make the software development as efficient as possible.

>"When cognitive load isn’t considered, teams are spread thin trying to cover an excessive amount of responsibilities and domains. Such a team lacks bandwidth to pursue mastery of their trade and struggles with the costs of switching contexts."

This resonates with me very much. I’ve considered before that the breaking point when I decide to switch jobs or domains is when I can’t handle the cognitive load anymore. I had that experience a couple of times already: I join a product team (I’ve never worked for a project based software company), we work together for a couple of years  and then we arrive at a point where we have e.g. 30 microservices to maintain, production incidents to respond to, interns to mentor and it all just becomes very difficult to handle. New members and even whole teams are usually hired during that period of time, but there is the thing with being one of the old-timers - people might want your input on things you built long ago. Or the thing with being a senior dev - at least I feel that I should pitch in not only in team scope, but also on the domain level. 

The authors suggest to combat this by:
- Limiting the amount of work assigned to the team. Mainly by defining clear domain boundaries and assigning them to teams following such heuristics: a single team should be able to accommodate 2-3 simple domains OR 1 complex domain. 
- Limiting the cognitive load not related with the business logic by creating platform, enabling or complex subsystem teams.
- Defining clear guidelines for communication between teams (collaboration, X-as-a-service or facilitation).

<ins>Platform and Enabling teams.</ins> From the above list the purpose of platform and enabling teams is the most interesting topic for me. [Platform engineering](https://devinterrupted.com/podcast/the-promise-of-platform-engineering/) seems to be a popular concept in the last few years, but different companies seem to define it rather differently. So I wanted to explore how it is defined in this book and how it is different from enabling teams. Here is what I found:

>"The mission of a platform team is to reduce the cognitive load of stream-aligned teams (similar concept to product or feature teams) by offloading lower level detailed knowledge (e.g. provisioning, monitoring, deployment), providing easy-to-consume services around them. <...> The platform team’s knowledge is best made available via self-service capabilities via a web portal and/ or programmable API.  <...> A good platform should make it easy for Dev teams to do the right things in the right way for the organisation. <...> Technology is only ever a part of the platform; roadmaps, guided evolution, clear documentation, a concern for DevEx, and appropriate encapsulation of underlying complexity are all key parts of an effective platform."

>"The mission of an enabling team is to help stream-aligned teams acquire missing capabilities, taking on the effort of research and trials, and setting up successful practices. <...> Jutta Eckstein calls them “Technical Consulting Teams”, a definition that maps well to what we’d expect a consulting team to provide (guidance, not execution)."



**What I disliked:**
I felt some confusion between the roles of platform and enabling teams. The responsibilities like provisioning, monitoring, deployment were mentioned in the definition for the platform team. But there was also this quote for enabling teams:

>"Often they are focusing on more specific areas, such as build engineering, continuous delivery, deployments, or test automation. For example, the enabling team might set up a walking skeleton of a deployment pipeline or a basic test framework combining automation tools and some initial scenarios and examples."

At the very end there was also a quote “organizations should expect teams to collaborate to discover new patterns and execution models, then push these down into the platform and supporting tooling”. This would suggest enabling teams collaborating with product teams and finding new ways and tools of working and then platform team converting them to a stable and mature service when the time comes. But this idea wasn’t expressed explicitly anywhere. Collaboration with teams to achieve as good developer experience was also mentioned for platform teams. 

The book is a very lightweight read. I’ve read it cover to cover and wrote down my thoughts in 5 days. I think it mostly serves as a good motivator to hire the authors as consultants for your organization. I imagine it to be a really long road to implement this in practice, especially in a large organization. A lot of the things mentioned here  are very complex. For example: finding the correct domain boundaries. I once participated in a two-day workshop with a Domain Driven Design guru dedicated to this very cause and I wouldn’t say I was very happy with the outcome. I believe it is a similar case with defining the boundaries of the platform. I’m afraid that if you encapsulate away too much from the developers they might lack knowledge to make the right decisions. There is also the question of resources. It would be ideal to have optimal cognitive load on each team so its members would also have the capacity to innovate. But there might not be enough developers in the organization and no resources to fill the gap.


