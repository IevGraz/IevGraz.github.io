---
title: Euruko 2023
location: Lithuania
date: 2023-09-30
---

Euruko is a Ruby conference organized annually, each year in a different European city chosen by the participants. This year it ended up in Vilnius because it was the 700th anniversary of the city and the participants were promised an event in [prison](https://www.lukiskiukalejimas.lt/pasivaiksciojimai/) and a custom Ruby beer. The prison turned out to be too small to host so many people, but they did get to taste a ruby colored beer made from beetroots.


### My relationship with conferences

I’ve been a Software Engineer for about 6 years now, but this was the first programming related conference I’ve attended. Mainly because it was an international conference taking place in Lithuania.  I had to partake in a lot of physics conferences back at university. It was never a pleasant experience for me as I always had to present a paper or even a talk on a subject I didn’t feel like an expert in. Once I changed fields and conferences weren’t mandatory in any way, I decided to skip them altogether. 


### TLDR: Useful links

* [Conference talks](https://www.youtube.com/@Euruko/featured);
* [Rabbit](https://rabbit-shocker.org/) - a Ruby based tool for creating presentations;
* A [gist](https://gist.github.com/schacon/a5da5f2e2e076eb2434f8775ac5ff55e) with a script to find which files usually change together with a specific file;
* [Rewind.ai](https://www.rewind.ai/) - a tool that allows you to record what you’re doing on your macbook and search it;
* A [blog](https://ivoanjo.me/) of a guy that is building a Ruby profiler @ Datadog.


### Reflections on the talks

**Day 1 Keynote: [Reflections on a Reluctant Revolution](https://www.youtube.com/live/iS-ReoqrWIY?si=HvLimRzFOGfwGkop&t=1630)** by [Steven R. Baker](https://stevenrbaker.com/). Steven is the creator of RSpec. It was the story of how he created and released RSpec and how he feels about it. For me this talk was good proof that programming is an art form. The speaker talked about the fears of being a one trick pony, the struggle of trying to create a better thing than the one you are known for and failing at it. This sounded very much like a struggle most creators (musicians, painters, writers etc.) could have.

**[No passwords, no problem. More passwords, more problems: Move beyond passwords with WebAuthn and passkeys](https://www.youtube.com/live/iS-ReoqrWIY?si=PF5Mnh8aVwiUNn2U&t=7389)** by [Carla Urrea Stabile](https://carlastabile.tech/). The speaker started the talk from a disclaimer that she _will be simplifying some things in her talk for the sake of clarity_. I loved this idea so much. I had someone comment on my post that “I got it almost right but not quite so” and clarify some things I actually knew. Disclaimer like that would have helped in that case. 

**Day 2 Keynote: A recording of [30 Years of Ruby](https://www.youtube.com/live/5WmhTMcnO7U?si=Vs9m3Qw1r7AyXQV_&t=1111)** by Yukihiro Matsumoto (Matz). It was interesting to see how important of a figure the creator of Ruby seemed to a lot of people. There was a lot of buzz around “Do you think Matz will be here?”, “We went to RubyKaigi and Matz was actually there in person!”. I didn’t really have similar feelings. Probably I don’t identify with being a “rubyist” that much. 

Even if prerecorded, the talk was really nice. He talked about parallelism and locking in very simple terms. It seemed like the case where a person understands something so well it is very easy for them to explain it. 


> **Rabbit gem**
    
> The most interesting thing for me was the slides though. They had a very fun “timer” at the bottom that showed a turtle and a rabbit racing. I was thinking how that was made when I saw a small text “[Powered by Rabbit 3.0.3](https://rabbit-shocker.org/)”. Apparently that is a Ruby gem for making slides and the slide progress tracking with a rabbit carrying a ruby gem is a default slide counter:

> ![Rabbit](/assets/videos/rabbit.gif)

> If you run rabbit with the `--allotted-time` flag than a turtle appears alongside the rabbit to show the progress of time:

> ![Rabbit & Turtle](/assets/videos/turtle.gif)
<br/><br/>

**[Ask Your Code](https://www.youtube.com/live/5WmhTMcnO7U?si=zKn91cqIgYq3IBak&t=6891)** by [Scott Chacon](https://scottchacon.com/about.html). He is the co-founder of GitHub and author of the official [Git book](https://git-scm.com/book/en/v2). This was quite exciting for me as I’ve read parts of the Git book and have found it very usefl. The talk itself focused more on ways of thinking  and raising the right questions. One of these questions was “Version control tools haven’t changed much over many years - how aren’t we frustrated by that?”. Then he analyzed potential useful questions that version control tools could answer for us e.g._ What files usually change with this file?_ This is a question I always have when I start to work on a new piece of code in an old repository. Git currently can’t answer this for us, but the speaker kindly shared a [gist](https://gist.github.com/schacon/a5da5f2e2e076eb2434f8775ac5ff55e) with a ruby and bash scripts that can.
He also mentioned the [Rewind.ai](https://www.rewind.ai/) app that he uses to record his screen and later search how he solved some problem previously.

**[Look out! Gotchas of Using Threads in Ruby](https://www.youtube.com/live/5WmhTMcnO7U?si=lmtwp1gxOJfRQcoo&t=9912)** by [Ivo Anjo](https://ivoanjo.me/). I was looking forward to this talk. Multithreading is a topic that I find rather complex and I enjoy every occasion to learn more about it. Sadly I got distracted by work and missed it. Luckily the speaker has [a blog](https://ivoanjo.me/) that I will definitely explore as he seems to enjoy digging deeper into complicated topics like performance tooling, global VM locks and, of course, threads. I should also probably watch the recording. 


### Final thoughts

Software engineering conferences don't seem to be a bad thing after all. Being there live in the audience forces me to focus on the talks more intently than I would if just watching them on my laptop. It is a good way to get introduced to new ideas or tooling and get a boost of inspiration and motivation. From now on I’ll try to visit at least one Software engineering conference a year. I heard good things about [QCon](https://qconferences.com/) and [StaffPlus](https://leaddev.com/staffplus-london). I’d like to visit one of them next. 
