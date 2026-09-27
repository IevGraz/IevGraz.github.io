---
title:  Mentoring again after a long pause (@WomenGoTech)
---

It has been 4 years since I last mentored at [WomenGoTech](/2022/04/28/women_go_tech.html). I find the activity meaningful, yet it took me a while to sign up for a new cohort. It got me thinking - why is that?

## Mentoring: how it is defined vs how I imagined it

With every mentoring opportunity (at WomenGoTech, at Vinted) we get an introductory course on what mentoring is and what we are supposed to do as mentors. Usually it focuses on active listening, asking open questions instead of leading ones and building a relationship.

But this leaves the technical part open to interpretation. The programme is about helping women get into tech, so surely there need to be some technical skills involved. How much of that is on me as a mentor and how should I approach it?

In the past, I used to stress about this a lot. I prepared presentations on technical topics and on what my work looks like. I even ran mock technical interviews. This made the mentoring period quite intense for me. Whenever a new opportunity presented itself, I would start to doubt if I really had the time and energy for it.

## How I wanted to approach it differently this time

Yet every time a new cohort was announced, I kept coming back to it. I would weigh the pros and cons over and over again. I took this as a signal that I still wanted to mentor. I decided to try again, but do it somehow differently. And that somehow was adding a note to my application that I would prefer to work on a coding project with my mentee.

I imagined that we would come up with a toy project together, do refinement sessions, prepare tasks in some free project board like Trello and then I could review pull requests. This would give the mentee practical coding experience and also shift the preparation work in between sessions onto them.

I also made a mental note to stress less about the 1:1 meetings. In the past I used to feel like I robbed the person if I didn't have enough content for at least 45 minutes. This time I intended to let the meetings take a more natural flow.

## The actual mentee and coding project

Adding the project note to my application turned out to be a great idea. WomenGoTech matched me with a person who already had a coding project in mind. And not just a toy project, but a real one, in a domain that I really care about.

The project is [Bogorm](https://bogorm.app/) - an interactive map of various reading events and places. It is meant to remind us that reading does not have to be a lonely experience. I connect with it immensely, as reading is one of my favourite leisure activities. For a while I even used to post book reviews to Goodreads and Instagram.

The author is [Liuba Kuibida](https://www.linkedin.com/in/liuba-kuibida/). She already had experience as a frontend developer, but wanted to build the backend for the app herself, and this is where I came in.

I don't think this match was a coincidence. It seems the organisers really do read the application notes. If you are thinking about applying as a mentor, take a moment to consider what you expect from the mentorship and how you like to work. Then mention it in your application.

## How we approached the mentorship

Liuba had coding experience and had also been both a mentee and a mentor before. She brought a lot of structure to our interactions, including SMART goals with a timeline set up in [Notion](https://www.notion.com/). We agreed on bi-weekly meetings. During these, we discussed what was already done and what could be an appropriate goal for the next check-in. This format was very similar to what all the mentoring workshops talked about - I listened actively and, where it made sense, shared observations and advice from my own experience. In between the calls, she would do the coding and I would review pull requests.

As for the 1:1s, the mental note helped. They weren't completely stress-free, but they were definitely calmer than before. We didn't have a fixed agenda and I didn't prepare anything in advance. Liuba would share her progress and ask questions, and the conversation would go from there. Some calls were short, and in others we drifted off to chat about unrelated things. I didn't feel I had to fill 45 minutes with content anymore, and I could actually enjoy our conversations.

This was much lighter than my previous mentoring experiences, and it still felt useful. It turns out the thing holding me back was my own definition of mentoring.

## Reviewing pull requests in a language I'm not familiar with

Liuba was already familiar with Python and Django, so we agreed this was the best tooling for the backend. I, however, have almost no experience with these tools. I did plan to learn them for [the project with my husband](/2023/11/03/coding_project_with_husband_pt1.html), but it never went further than a plan. Luckily, in the age of AI this wasn't a big problem. I have a [Claude Code subscription](https://claude.com/pricing) for my personal needs. I would run `/code-review` on the project, browse the output and look for things I could turn into a general lesson on backend engineering, e.g.:

- having different configurations for testing and production environments
- using libraries like [factory_boy](https://factoryboy.readthedocs.io/en/latest/index.html) to generate test data in the most readable way
- having the correct separation of responsibilities between models and views (Django's version of controllers)

Of course, reviewing code in a framework I don't know had its risks. AI can be confidently wrong or miss the context of the project, so I was picky about what I passed on. I mostly focused on issues I recognised from general backend engineering. When the AI flagged something and I couldn't see why it was a problem, I dug deeper and asked for links to the documentation. Sometimes I also turned things around and asked my own questions, for example whether the project's split into Django apps followed the framework's conventions.

Whenever an issue seemed like an opportunity for a broader discussion, I added the documentation or other resources I found to my comments, so Liuba could read up on the topic herself.

## Sharing my AI skills

The mentorship lasts 6 months, but the project needs more time to be fully finished. During the second half of our collaboration, I wanted to guide Liuba towards doing the AI reviews on her own. I shared my process with Claude Code, plus a new review skill I started using recently - [/ponytail-review](https://github.com/DietrichGebert/ponytail/blob/main/skills/ponytail-review/SKILL.md). It complements `/code-review` nicely, as it focuses on code that can be removed, like duplication or things the framework already provides. This helps keep the code clean and DRY, and cuts down on AI slop when some of the code is AI generated.

## My biggest takeaway from the programme

When programmes like WomenGoTech look for mentors, they usually advertise benefits such as new connections and the chance to learn by explaining things to others. What I got was something different, and I don't think it gets mentioned nearly enough: motivation. For 6 months I watched Liuba move steadily towards her goals and hit small milestones, like deploying to production for the first time and seeing the app live. It pushed me to get back to my own projects: reading technical books, writing this blog and working on the book-related coding project with my husband. I have been more consistent with them than I have in years. Every two weeks, our check-ins reminded me that a couple of hours a week is all it takes to keep getting closer to the goal.

## Check out Liuba's work

| Link | What it is |
|------|------------|
| [Portfolio](https://portfolio.liubuntu.tech/) | Liuba's portfolio |
| [Blog](https://blog.liubuntu.tech/) | Liuba's blog |
| [Bogorm](https://bogorm.app/) | An interactive map of reading events and places, the project we worked on together |
| [RESHETO](https://ni4yja.github.io/re-she-to/) | Data on translated books in the Polish book market from 2000 to 2025, another project she built during the mentorship |
