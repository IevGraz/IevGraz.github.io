---
title:  Talking about Software Architecture for the women @WomenGoTech
---

This year I have been selected as one of the experts to talk about different areas of Backend development for  the mentees at [WomenGoTech](https://womengotech.com/). I chose the topic 'Software Architecture' as this is something I’ve been reading a bit about [recently](book_reviews/fundamentals_of_software_architecture.html). This was a big thing for me, as I rarely get to speak publicly. Especially for a cause that I care about so much. I invested almost 2 months (more on this in the [Reflections](#reflections) section) for the preparation as I wanted to make the talk as good and useful as possible. And now once the talk is done I want to reflect on it a little.

## The requirements

At the beginning of this WomenGoTech season all the experts were invited into an introductory session and given the following requirements:

| **Duration:**      | 1,5 - 2 hours       |
| **Goal:**   | Guide mentees to the right direction rather than fully prepare them for certain roles and responsibilities        |
| **Mentee profile:**   | None of the mentees work as backend developers as of yet, majority of them have completed Code Academy or similar        |
| **Pro tips:**   | Aim for the session to be as practical as possible, do not repeat the content that is easy to find online        |
| | Include different activities to engage the audience      |

## My resources



* My experience: I have worked with different architecture styles so I have some practical experience with monolith vs microservices, event-sourcing vs storing the final state, request-response vs messaging. 
* My recent deep dive into various resources about Software Architecture


## My take

While reading the mentee profile and thinking about various aspects of the Software Architecture I could talk about, I had flashbacks of super technical talks about topics I have no experience with yet. Those usually left me feeling overwhelmed and doubting my competence. And the requirements did state that my goal is to guide them in the right direction rather than make them experts of Software Architecture in one night. So I decided that instead of jumping straight to explaining _‘the what’_ of the Software Architecture I want to focus on _‘the why’_ they should even care about the topic at this point. Or not only at this point but at different phases of their career:

1. At the first job 
2. Looking for the next job
3. Choosing path for further career

And these were the main sections of the talk.


## The talk

The initial draft of this post contained full notes for the presentation in this section. I used it to gather some feedback from actual Software Architects. But it was way too much text for a post, so I will just summarize the structure of the talk instead. 

The first section ‘At the first job’  was also the meat and potatoes of the talk where I presented all the theory that I wanted to share. I relied on the definition of Software Architecture as the system level decisions (or the big decisions you make before you start coding) that are hard to change after you implement them. I divided these decisions into 3 groups:

**Decisions about the structure of code.** Here I introduced the different types of architecture styles (Layered, Modular Monolith, Hexagonal etc.), explaining the first two in a bit more detail.  
_Why is this useful for a fresh dev at her first job?_ I think if you find out which architecture style is used in the project you will be working on and read a bit about it, it will be much easier to navigate existing code and decide where to put new code. 

**Decisions about the deployment of code.** Here I introduced different ways (vertical vs. horizontal) to scale your production infrastructure as well as monolithic vs. distributed architectures with their pros and cons.   
_Why is this useful for a fresh dev at her first job?_ If standard architectures like microservices are used in the company there probably won't be much documentation about the architecture style internally. But there is plenty on the internet, so it is good to know that there are resources to help you understand some terms and concepts faster.  

**Decisions about communication of code.** For the distributed architectures it is also an important decision how different parts (services) in the architecture should communicate with each other. Should they request-respond synchronously or talk asynchronously via messaging. So I introduced the two communication styles briefly. I also made a little detour into explaining the concept and properties of Restful APIs. As I think it is likely there will be tasks of consuming or creating APIs for a fresh dev and it is good to know that there are standard practices/ recommendations about this on the web. 

Since the talk was also required to include different activities to keep the mentees more engaged, I created a short quiz after each of these subsections. I tried to reiterate my main points in 2-3 multiple choice questions. I thought this would give a short pause to let the information sink in. As well as be an opportunity to present the message one last time in a bit different way.  

I also wanted to do a more engaging, practical assignment. I decided to go with an [architectural kata](https://nealford.com/katas/) about building an online auction.  I presented the requirements and then gave mentees some guiding questions to discuss in groups. With this task I also wanted to encourage the women to participate in technical discussions from the very beginning. As I notice this is something junior developers often fail to do yet it could be very beneficial for their growth. 

The last two sections of the talk were very brief, mostly just to provide some resources and advice. As another place where you might get to discuss Software Architecture is system design interviews, I gave a reading list on how to prepare for them. We also discussed various career paths one can choose after being a backend developer for a while and the different profiles of knowledge needed for an architect (breadth of knowledge) vs a good specialist/ individual contributor (technical depth) and a possible routine on gaining that knowledge little by little, 20 minutes a day. 


## Reflections


### Preparation phase

As I mentioned in the introduction, I spent around a few months working on the presentation. Of course, it wasn’t a continuous effort - more like few hours a week spent on the slides and a bit more just thinking about them. But this is a common issue I have with presentations. [The Pareto principle](https://en.wikipedia.org/wiki/Pareto_principle) would suggest 20% of effort would create 80% of the desired result. But I get carried away with tweaking the details, especially the visual ones. This is a habit that I would really like to break as sometimes it leads to me refusing opportunities, knowing how much time and effort they would require.

After all this effort, I was pretty pleased with the result. I sent out the draft to people more experienced with Software Architecture. And I got quite a few comments! Most of them focused on tailoring the presentation to my audience and making it more simple. I had to sit a little with the feedback (as I might have been expecting something more along the lines of ‘great job’ instead) but then I realized what happened. I got carried away with making the slides look pretty and forgot the initial goal I set for myself - making the talk clear and accessible. I asked for the feedback quite late so didn’t have time for any major changes. I added slides to explain the vocabulary and some concepts in very simple terms and I think that really helped the end result. It also made me realise the value of feedback, especially for things I’m creating completely on my own.

While preparing for the talk I have also found out how much practice I need to be able to speak fluently enough without reciting the entire thing from memory. I ran the talk once alone with a timer and then once more in front of someone (sort of a light version of public speaking stress). And that did the trick! In this case the someone was experienced in public speaking so as a bonus I got useful tips: to add numbers to the slides so listeners could note them for questions, to remove any unnecessary text that would only serve as distraction, etc.


### The actual talk 

I remember a short story Brene Brown told in her book ‘The Power of Vulnerability’: in the situations where she doesn’t really trust her automatic reactions, she takes a pause to spin a ring around her finger and that is usually enough time to create space for continuous, mindful reaction. I was missing a pause like that before I started to speak. Only around halfway into the presentation I realized I’m not even sure if I'm sharing full screen or just a tab. If I had made a small pause to collect myself, it could have been a bit more smooth.

Comparing theoretical vs practical parts of the presentation, I could see that the women were more engaged in the later ones. Which completely makes sense as listening to someone talk for an hour in the evening can be quite tiring. And indeed this was the main advice from WomenGoTech organizers - to make the presentation as practical as possible. But I fully comprehended it only after seeing the different level of engagement myself. If I got to redo the talk now I would think hard about how to express more of the theory through some exercises. 

I also would go about the architecture kata assignment a bit differently. After assigning the mentees into breakout rooms, I waited 5 minutes before joining the rooms, to give them time to brainstorm in peace. Unfortunately, the assignment turned out not to be as clear as I expected and the groups would have benefited from me joining them as soon as possible. I learnt from this mistake right away and made sure to check in often and give a nudge in the right direction if needed. 


## Feedback

WomenGoTech asks their mentees to fill a feedback form after each talk and share the summarized results with the speaker. After noticing all the things I could have done better I was really looking forward to it, to see if mentees also noticed them. But the feedback was overwhelmingly positive - the score  was 5/5. That immediately made all the effort I put into this completely worth it.
