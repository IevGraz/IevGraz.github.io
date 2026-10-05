---
title: DevOpsDays 2026
location: Vilnius, Lithuania
date: 2026-09-30
---

To be completely honest, I've been feeling overwhelmed with everything happening in the world these days (AI, layoffs, the war in Ukraine), and arranging a trip to a conference abroad seemed like too much. But I still wanted to stick to the idea of visiting at least one conference a year. So I attended [DevOpsDays](https://devopsdays.lt/) in Vilnius. I appreciate that it is not a profit-oriented event and any leftover profits are donated.

This was the 4th time the conference was organised. It lasted 2 days and consisted of 5 x 40-minute talks, 4 x 5-minute ignite sessions, and open space discussions (which I skipped).

## Reflections on the talks

### Day 1

I won't discuss every single talk here, just the ones that stood out to me the most.

<ins>[Jan Moser](https://www.linkedin.com/in/moserjan/) – How we build an airport with AI</ins>. One genre of videos that I like watching on YouTube is megaprojects - various architectural ideas that are innovative either in their construction or in their social implications. I watch these on channels like [TheB1M](https://www.youtube.com/@TheB1M) or [Megaprojects](https://www.youtube.com/@megaprojects9649). This talk would fit nicely into one of those. The use of AI is two-fold here: in the daily operations of the airport as well as in producing documents for building it. The daily operations part is rather scary. The airport is being built in Vietnam, where the privacy policies are lax, and there will be a lot of biometric tracking and human recognition algorithms applied.

The document part was a lot more mundane. AI was used to generate some 700 000 lines of markdown that were eventually turned into construction specifications. I assume they worked on this for a while, through various stages of model quality, so the lessons learned seemed quite simple. Use version control, so AI does not destroy some files you care about. Use git repositories to make sure multiple people can collaborate successfully, etc.
One really good reminder was to not default to using LLMs for everything. Sometimes it is much cheaper and much more practical to use an LLM to help you write a script that you can then simply re-run and get a good, deterministic output. Let's not forget our developer skillset and mindset!

<ins>Grzegorz Kalwig – Wrong tool, Wrong Quest: What IT Teams Can Learn from RPGs</ins>. I feel that with the current AI image generation capabilities, every conference now has at least one talk where people try to merge software engineering practices with fantasy/RPG themes. I'm not a big fan of this approach, as the rich visual theme may drown out the actual technical message.

![Project roles as RPG character classes](/assets/images/devopsdays_rpg_roles.jpg){: width="700" }

But one thing I liked in this talk was the stats for various aspects of systems (operational excellence, security, reliability, performance efficiency, cost optimisation, sustainability) - the six pillars of the [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/). I think the levels of excellence were captured well in these. A few examples:

| Points | Operational Excellence | Reliability | Security |
|---|---|---|---|
| 1 | Manual deployments, no structured logging | Single-AZ deployment, no failover | Basic IAM roles, default settings |
| 2 | Basic CloudWatch alarms, semi-automated scripts | Multi-AZ, simple retry logic | Separation of environments, WAF |
| 3 | IaC (SAM/CDK), versioned deployments, basic CI/CD | Failover strategy + DLQ, backup & restore in place | Fine-grained IAM, Secrets Manager with automated secrets rollout |
| 4 | Full CI/CD pipelines with rollback, metric-based alarms | Cross-region backup, chaos testing | Policy boundaries, Shield Adv., MFA enforced |
| 5 | GitOps/IaC + self-healing + automated chaos experiments | Warm standby multi-region architecture | Zero trust, automated compliance checks (Config/SCPs), audit logging |

The argument was that, as in RPG games, you are not allowed to set every stat to the maximum value. In real engineering life, time and money stop you from doing the same with your system.

<ins>Saulius Valatka – V-Assist: AI agents for all at Vinted</ins>. I work at Vinted, and I use V-Assist daily, for almost every single thing I need to do. I'm a huge fan of it. But what I appreciated most in this talk was Saulius' honesty about the current state of working with AI. The gist of it was that individual developers may feel like 10x developers with AI. In the bigger picture, though, the pace of delivering big initiatives is mostly unchanged. This is because the structure of the work is still the same. We attend meetings, agree on things to do, refine the implementation details, and then pass them on to an agent to implement. We wait for the agent to do something, watch YouTube during the idle time. Give feedback, rinse and repeat. At best we might scale to running several tasks like this at the same time. But then we pay the huge price of context switching. Humans are generally the happiest when they are able to achieve deep work. So it would be ideal if we could have a focused design session, then give it to AI and move on to other things, without needing to check in constantly.

<ins>Konstantinas Jurgilas – So You Want to Replace a Platform: Lessons Learned from Inside the Trenches</ins>. I want as many talks like this as possible. People making a big, long-lasting change to widely adopted internal tooling and then sharing their reflections afterwards. I think it is very valuable, as this is something platform engineers have to do often, so the more we can learn from others, the better.

The first part of the talk was dedicated to the 'people' side of things. I loved the idea of a 'resistance budget'. Similar to how errors eat at your SLO budget, bugs and missing feature parity will eat at the resistance budget (maybe it should be called a patience budget?). Improvements and well-provided guidance, on the other hand, will increase it. The suggested forms of guidance were:
- document how-tos, tips & tricks, and workflows for moving from the old platform to the new one
- host office hours for live support
- create example migrations - real assets to copy-paste from

For the technical part, the emphasis was on automation. The automation can be done with AI skills and MCP servers. I've been a part of several migrations where a bunch of teams had to adapt to new tooling. Often we provided documentation and asked them to implement and verify. It could have been so much simpler with AI tools! We could have easily written AI skills to do the code changes. They are usually very specific steps of replacing X with Y and renaming some ENV vars. AI could also automate the process of applying this to every repository and opening pull requests for teams. Furthermore, given a specific checklist, it could monitor Grafana dashboards for anything out of the ordinary. An important point delivered in this talk was that if we are automating the execution, we should also automate the verification. Otherwise it becomes the bottleneck.

### Day 2

I noticed a tendency with events that last multiple days. During the first day I absorb a lot more information, but I also get overstimulated and don't sleep as well. On the second day I'm really tired and find it much harder to enjoy the event. It's the same energy drain I wrote about after [GoLab](https://www.ieva.dev/conferences/golab_2024.html). I think this is part of the reason only one talk really stuck with me on Day 2.

<ins>Josephine Pfeiffer – Touching Grass (and 40-year-old C code)</ins>. Josephine is one of the maintainers of the [NetworkManager](https://gitlab.freedesktop.org/NetworkManager/NetworkManager) project. She spoke about the pains that AI has caused for the maintainers of open source projects. Before AI, comprehending and writing code was the bottleneck. People took a while to make a contribution. Now, they can copy-paste an issue description to Claude and have a pull request ready in no time. Or a slop grenade, as Josephine put it. It seems the AI-generated pull requests are big, and the communication is poor - even the replies are written by AI. It has become so problematic that she wrote a policy for the use of AI agents that included the tenets "Write your own commit messages and Merge Request descriptions. Respond to review comments yourself.". To make it easier to catch the people who do not comply, she also added an instruction to AGENTS.md to add the word _biblioklept_ whenever AI is the one generating the description. This got her a bit of attention on [Phoronix news](https://www.phoronix.com/news/NetworkManager-AI-Canary). Mostly this was a fun story to hear. But I also see merit in keeping the communication layer fully human.


## Reflections on the ignites

The ignites were speed talks where the presenters had to prepare 20 slides that would flip automatically over the span of 5 minutes. Most of these were nice quick ideas that I don't have much to reflect on. Except for __Lina – Seeing Through the Noise: Quality Is Imperfect__. Within those 5 minutes she managed to beautifully capture and express the frustration of being served a lot of slop as a human being. I suppose this hits QAs extremely hard, as they get AI-generated features and bug reports. But I guess we have all been in situations where a counterpart in a discussion just copy-pastes an AI-generated response. This is how pages like [no-slop.ai](https://no-slop.ai/) are born. I'm so upset that the agenda does not include Lina's full name. I would like to let her know how great an impression the talk left on me. And maybe get hold of the poem she ended the talk with.

## Resources

- Charity Majors' [Substack posts](https://charity.wtf/profile/posts) (mentioned by Lina in her ignite)
- Konstantinas Jurgilas' [blog](https://jurgilas.blog/)
- Josephine Pfeiffer's [blog](https://josie.lol/blog/)


## Final thoughts

This conference is actually a gem that more foreign DevOps engineers should discover. It is cheap (~100EUR). The venue was unique - [Kablys](https://www.mankablys.lt/). The talks were proper (a lot of international speakers). There were warm meals for lunch. If you wanted to, you could start buying beers from 2 P.M. (and the evening beers were free of charge).
