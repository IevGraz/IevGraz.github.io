---
title: DevOps in Shorts 2025
location: Vilnius, Lithuania
date: 2025-05-10
---

[DevOps in Shorts](https://www.devopsinshorts.com/) is organised by DevOps enthusiasts for DevOps enthusiasts. It’s supported financially by various companies, so the attendance is free of charge. This was the fourth time it happened. First time around 25 people gathered. Each year the number of participants grew by around that same number reaching 100 this year. I found out about it from one of my colleagues who was a part of the organising team. 


## Reflections on the talks

There were 11 talks in total, each lasted up to 15 minutes + 5 extra minutes for answering questions.

My favorite one by far was “**Cloud Native, the Hard Way: Mistakes from Our VM to K8s Journey**” by Augustinas Šimelionis. The key takeaway I wrote down from this talk was “*Never assume people actually know kubernetes*”. It was illustrated by examples of people not knowing anymore on how to connect to their deployments or how to assign resources for the pods and configure the autoscalers. The key remedies listed by Augustinas were:

* Sane standards and defaults
* Well documented happy path
* Learning sessions between SRE and backend guilds.

This reminded me of when I was a software engineer and our deployments were migrated to Kubernetes by infra teams. Infra teams prepared examples and default configurations for us, but we usually copy-pasted them without really understanding what things meant. The real understanding came when things stopped working as expected due to the copy pasted values. 

The second best talk was also about Kubernetes: “**VPA + HPA workload optimization**” by Aivaras Atkočaitis. Mostly I liked the author's approach to the talk - he took a very specific problem (configuring the HPA autoscaler for different types of loads: stable, seasonal and spiky), provided examples of configurations and discussed their pros and cons. For example, when configuring HPA for an app with seasonal workloads you can choose between:

<ol type="A">
  <li>Requesting a little CPU for single pod (e.g. 0.25 CPU), but allowing the autoscaler to scale pods in a wide range (e.g 2-100)</li>
  <li>Allocating a bit more CPU to a single pod (e.g. 1 CPU) and then needing less pods to cover the full load (e.g. up to 30)</li>
</ol>

In the first case you will allocate less resources, but will have a lot more upscaling/ downscaling events that can be destabilising to your apps performance. In the second case you are overprovisioning a bit for the sake of stability. A similar analysis was done for other types of workloads - a clear, short talk. 

There were two more talks that weren’t that relevant for me, but I appreciated them being there. The first was a presentation on the **Cybersecurity Unit "Lizdeika" of the Lithuanian Riflemen's Union**. I really liked how much interest it received. It got  the most questions and afterwards the speaker was surrounded by people for almost the entire duration of the break. People seemed interested in using their skills to serve our country. The second - “**Why is everything always broken**” by Ignas Poškus. If I understood correctly, this was based heavily on the book [Wiring the Winning Organization](https://www.goodreads.com/book/show/125164532-wiring-the-winning-organization) and suggested that the answer to the question in the title is “because of the cult of speed”. If organisations managed to slow down a bit, they could gain more control over what is happening and remove many friction points. I get stressed out by how often and fast things change at work, so I appreciated the message. It would be interesting to read the book and find out more as the talk was too short to give any insights on how this would really look.


## Reflections on choosing the right audience for your talk

There were some talks about the definition of DevOps and Platform teams. I found these a bit puzzling, as the majority of the people in the conference are already working in the field and are familiar with the terms. Platform engineering is also not a new thing. I remember reading a post called “[The Future of Ops is Platform Engineering](https://charity.wtf/2022/09/30/the-future-of-ops-is-platform-engineering/)” back in 2022. I attended the event with my husband and we were talking during the break about this. He suggested an interesting idea - maybe people should mingle a lot more when choosing a conference (both as attendees and as speakers). Now we attend a DevOps conference and a lot of talks get questions like “how to sell this to management” and maybe managers are attending conferences where they discuss how to focus DevOps on doing what needs to be done and stop looking for shiny new things. Maybe talks that present the idea of Platform teams and how they should function would do better in a conference for engineering managers. 

A stark example of this was a talk called “Debunk the myth about external DevOps teams”. It prompted a lot of “cultural” questions like “Are you sure this is the right audience for this talk? Convincing DevOps that you want to replace them? Better audience would be C level managers”.


## Resources

A few resources I’ve heard about during the conference:

Book recommendations:
- [Wiring the Winning Organization](https://www.goodreads.com/book/show/125164532-wiring-the-winning-organization)
- [Rojalio kambarys (fiction)](https://www.goodreads.com/book/show/17828089-rojalio-kambarys?from_search=true&from_srp=true&qid=I0VPaEiKVZ&rank=1)
- [The Making of a manager](https://www.goodreads.com/book/show/38821039-the-making-of-a-manager?from_search=true&from_srp=true&qid=cdySICk5kj&rank=1)
- [Managing Humans](https://www.goodreads.com/book/show/1317946.Managing_Humans?from_search=true&from_srp=true&qid=i6OJNFh3ix&rank=1)

Other conferences to attend:
- [DevOps Days (Vilnius, Lithuania)](https://devopsdays.lt/)


## Final thoughts

I love that this conference exists! I find the format (happening on a weekend, in a quiet place by the lake) to be more motivational than educational. And that is great. It is a place to hangout and relax with other people from the same background and get to feel more inspired about the work that you do daily. Organising this is a fully volunteer activity and the organizers are pouring a lot of their free time and energy into this. It is possible to [support them ](https://ko-fi.com/devopsinshorts)a bit as a thank you. So I did. I suggest that next year you should visit the conference, get inspired and buy them a coffee.

![Buy DevOps in Shorts a coffee](/assets/images/shorts_kofi.png){: width="700" }