---
title:  'Coding project with my husband: part 1'
---

My husband and I started to work on a coding project together. I want to share some reflections here.

**How did it start?** Few years ago my husband started switching careers to software engineering. I was eager to help but it soon turned out I get annoyed if I can’t figure out a way to explain things. At that time we left it at that and I mostly contributed by recommending books and other resources. But I still felt bad in the back of my mind. Recently I suggested we should try to do a project together in order to practice constructive collaboration. 

**What do we want to create?** We settled on building a service that would help to track our “book challenges”. We have a tradition where one of us chooses 2 books that are somehow related (same author, topic, etc.). Each of us reads one of them, then we swap and finally we plan a date to discuss our impressions. It can take several months for both of us to get through both books, so we take notes. Usually on random pieces of paper. Therefore it would be nice to have all the information - current and past reading challenges, notes taken - in one place. The working title for this project is “BookBuddy”.

![Book challange flow](/assets/images/book_challenge.drawio.svg){: width="1080" }

**How do we approach it?** We set up a typical software engineering workflow process: a Jira board for the project connected to a GitHub repository; a backlog of ideas and a kanban board for things we are currently working on. Before creating any tasks we had a few discussions on what we want to do and how. Initial plan was that I will learn some Python and Django and then we will start collaborating on the tasks. 

![Our jira board](/assets/images/bbd_jira.png)

**First impressions:**
_Different goals_. When we started talking about what we wanted to do exactly, it became clear that we had completely different goals. Mine was to practice collaboration and maybe test if a similar approach could be used when mentoring. He, on the other hand, was focused on the result - how to create something that we could actually use and test as soon as possible i.e. choosing the correct minimum viable product. 

_Importance of trust_. A lot of texts on healthy team dynamics emphasize the importance of trust among the team members. This exercise helped me to experience that first hand. When discussing things at work, I usually have at least a tiny bit of impostor syndrome dialogue running through my head. Yet it wasn’t there during technical discussions with my husband. 

_Working on what I actually enjoy_. As I mentioned before, the initial idea was that before we start coding, I will learn the basics of Python and Django. Yet I kept on stalling to the point where my husband started to code alone. I had to admit I don’t have the motivation for learning a new language at the moment. I felt some inspiration only when I decided that it would be cool to trigger a test run on pull request build. On this I easily spent multiple hours until I got it right. This proved again to me that I’m more interested in platform things at the moment. 

**What’s next?** We are currently at the very beginning of the project. Our goal is to have a working product with some user interface and accessible via network. For the UI we are considering using the [GPT pilot](https://github.com/Pythagora-io/gpt-pilot) and see how capable AI currently is. If we’ll want to use this project for learning purposes longer we might try to add things like a search mechanism, book information import, calendar integration for scheduling the book talks etc. I really hope there will be more interesting experience to share on this blog.
