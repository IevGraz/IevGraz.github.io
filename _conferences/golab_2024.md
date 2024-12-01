---
title: GoLab 2024
location: Florence, Italy
date: 2024-11-14
---

Golab was organized for the 9th time this year. It seems to always take place in Florence, Italy. I  started learning Go recently and had the idea that this conference might help me on my learning journey and give me a chance to mingle with other, more proficient,  Gophers from my company. 


## Reflections on the workshops

The first day of the conference was dedicated to workshops. There were 3 tracks of workshops:

| I  | II | III |
| ------------- | ------------- | ------------- |
| Go design principles for better Go development  | Fyne apps from start to store  | A simple approach to secure code |
|   | Exercises in performance optimizations  | Go testing boot camp |

I signed up for the first one, without really reading the description, because based solely on the title I expected it to be a guide for writing tidy real life applications. Something along the lines of ‘if you have a big Go project, this is how you should structure it and these are the patterns you should apply to your code’. From what I gathered from various conversations, I was not the only one with this assumption.

In reality the workshop focused on 3 of the more complex topics of Go - interfaces, generics and concurrency. The materials of the workshop can be found [here](https://github.com/ronna-s/go-design-workshop/tree/main/lessons). The first lesson was my favorite one by far and my favorite thing from the entire conference. It aimed at introducing important concepts for Go interfaces via implementation of a quirky terminal game where a Minion, a Gopher and a Rubyist can cast some actions towards production. We had to implement the characters and the game loop. 

I find terminal games like this really exciting. The only other thing I ever coded with Ruby in my free time was also [a game in the terminal](https://www.ieva.dev/2021/11/28/game_of_life.html). We didn’t manage to finish the game during the workshop, so I spent the evenings after the conference working on it. I managed to get it working by last night:

<video width="640" muted autoplay controls >
    <source src="/assets/videos/go_game.mp4" type="video/mp4">
</video>
<br/>

I found the following requirements the most useful:

* A minion doesn't have a method `Alive() bool`, but it needs to satisfy the Player interface, so we can initialise the game with array of players.
* If an unsuccessful move was made against PRODUCTION while in legacy mode, one player will be terminated at random (except for Minion, minions can't be fired). 

The first one was a hint at the pattern used by [NopCloser](https://pkg.go.dev/io#NopCloser) that was also mentioned in the Learning Go book. It was nice to be forced to actually implement this and not only read about it

The second one got me stuck for a good couple of hours. “Terminate” felt like an “update” operation, so I wanted to implement this via isAlive flag on Player: 

```
func (r *Rubyist) Terminate() {
   r.isAlive = false
}
```

At first I forgot that if I need my method to modify something on a type, the receiver has to be a pointer type. After fixing this it still didn't work, as it seems I also need to check the property via a pointer as well


```
func (r *Rubyist) Alive() bool {
   return r.isAlive
}
```


That led to needing to instantiate the Rubyist and Gopher players as pointers:
```
func NewRubyist() *Rubyist {
   return &Rubyist{isAlive: true}
}
```

I didn’t like that very much. This is not needed for Minion types and leaves me with a mix of value and pointer types in Players array. It feels like something that people could easily forget or overlook if the code had to live for a long period of time. I talked about this with a colleague and he suggested that a nicer way might be for the terminate method to just return a new instance of Player, with the correct state. So I changed my implementation to this:


```
func (r Rubyist) Terminate() pnp.Player {
   return pnp.Player(Rubyist{isAlive: false})
}
```


And then the code that invokes this method:


```
randomIndex := rand.Intn(len(g.Players))
player := g.Players[randomIndex]
if player.Alive() {
   if terminator, ok := player.(Terminator); ok {
      g.Players[randomIndex] = terminator.Terminate()
      break
   }
}
```


It does work as expected. I like it a little more. The only minor issue I have with it is casting the concrete type to the Player interface.

I realised it really requires a shift of mindset for me to start coding the Go way - modifying the flag in Ruby would have been a no brainer.


## Reflections on the talks

The top 3 talks for me were:

The keynote talk “**Go Telemetry Wins**” by **Russ Cox**. Russ Cox is one of the people working on the Go programming language and he seems to even have been [the tech lead](https://news.ycombinator.com/item?id=41132669). He also has the best Go themed shirts I’ve ever seen. I tried to google them, but couldn’t find them.

![Russ Cox](/assets/images/golab_presentation_cox.jpeg){: width="375" }

He presented why and how they implemented metrics to collect data about Go toolchain programs’ performance and usage. 

**The why:** Software quality is its usability + reliability. You can try to gather information about this from developer surveys and bug reports. But these methods are costly and not always reliable. Having actual metrics can provide much better data.

**The how:** gathering metrics from users’ workstations have many issues - it might feel like a violation of privacy, it might require storage space on users computers and cost them extra bandwidth to send it. There are also issues with power imbalance when deciding who can access the data. Russ Cox shared how they addressed all of these points:


* Privacy: only counters and values are stored;
* Cost: metrics are gathered as a weekly summary - a few kB upload once a week;
* Consent: go telemetry is opt - users choose if they want to participate;
* Power Imbalance: the metrics are available for all at [https://telemetry.go.dev/](https://telemetry.go.dev/) 

Another neat fact from this talk was that they calculated that they need 10 000 reports per week to have reliable data and they have a configuration file to control the sampling rate. Once more people opt in, less data will be needed from each of them. 

“**Watermill: the missing standard library for event-driven applications**” by **Robert Laszczak**. It wasn’t as much the talk itself that I liked, but the library that was presented. Recently I’ve spent some time looking into Go libraries for communicating with Kafka and sadly completely missed this one. Most likely because I was googling strictly for Kafka clients and Watermill is rather universal - it can be used with Kafka, RabbitMQ, Redis, Sql, etc. 

The most popular Go Kafka clients ([sarama](https://github.com/IBM/sarama), [confluent-kafka-go](https://github.com/confluentinc/confluent-kafka-go), [segmentio/kafka-go](https://github.com/segmentio/kafka-go)) don’t really provide any additional functionality like [dead letter queues](https://medium.com/@danthelion/dead-letter-queues-what-they-are-and-when-to-use-them-252c33fb4ced), hooks for telemetry integration etc.  on top of message publishing and consumption. Watermill, on the other hand, has a lot of convenient functionality:


* It provides [middlewares](https://watermill.io/docs/middlewares/) for circuit breakers, dead letter (poison) queues, retries etc;
* It has a [Prometheus metrics implementation](https://watermill.io/advanced/metrics/) and an easy way to register decorators like this for all consumers and producers; 
* The creators seem to specialise in Domain Driven and Event Driven designs (and [provide courses](https://threedots.tech/learn/) for it) so the library also has a nice [API](https://watermill.io/docs/cqrs/) that implements those concepts.

It seems the library is used and liked in the Go community. There were people in the audience who instead of asking a question just wanted to tell the authors they use the library in production and really appreciate it. It was also mentioned in other talks. 

“**From Bland to Spiky: How Generics Made My Service Super Robust**” by Teea Alarto. This was the talk where I was more by the form then the content itself. More precisely two aspects of it:

**Visual style**: The presenter aligned the visual aspects perfectly. She adjusted her VS Code style (used to present some code snippets), to match that of the slides. I even approached her to ask what she used - the font was[ Operator Mono](https://github.com/willfore/vscode_operator_mono_lig) and the theme - [Night Owl](https://marketplace.visualstudio.com/items?itemName=sdras.night-owl). She also used [Night Cafe AI](https://creator.nightcafe.studio/) to generate the illustrations.

**Presentation style**. Teea Alarto shared about her experience of working with generics. For someone like me who has very little experience with generics in Go they look very complex and hard to read. I really appreciated that she shared that she had very similar impressions at first and how she iterated on her solution. I admit I struggled to grasp it fully during the conference, but she shared her [repository with all the iterations](https://github.com/teeaa/generics). I’m still hoping to spend some time looking into it. 

I also appreciated that in her talk she made a parallel between a hedgehog running a pie factory (those were the images generated with [Night Cafe AI](https://creator.nightcafe.studio/)) and her journey with generics. The switches to hedgehog world gave nice shorts breaks for the brain during the talk.


### Inspiration

Some talks didn’t seem that useful for me work-wise but they were a good inspiration of what topics could be covered in other settings and how. I used to be a mentor at a local [Women Go Tech](https://www.womengotech.com/) community. I haven’t done that in a while but I start to think I would like to get back to it and there were a few talks that gave me inspiration on what I could do differently next time. 

**“Let's Go Asynchronous”** by Tomáš Sedláček had a really nice way of explaining asynchronous communication and when it might be useful. He did this through a real world example of a Gopher running a jewelry store and printing invoices for his clients. He developed the example by upgrading the printer used. Eventually Gopher could start a printing job and get back to his clients and the invoice would be sent to them automatically. Now he was able to serve so many clients and one printer was no longer enough. So he had to buy more and make sure that work was sent to them correctly. This led to a pretty good explanation of possible issues with asynchronous communication. 

![Async Communication Drawbacks](/assets/images/golab_presentation_async.jpeg)

I once did a [talk about Software Architecture](https://www.ieva.dev/2022/04/28/women_go_tech.html) for the mentees of Women Go Tech. I based it on the contents from the book “[Fundamentals of Software Architecture](https://www.ieva.dev/book_reviews/fundamentals_of_software_architecture.html)” and looking back to it I think it turned out rather dry and complex. If I ever have to do something similar again, I’ll try to frame it in a similar way Tomáš Sedláček did in his talk.

**“Graphs and games: can Go take a Ticket to Ride?”** by Michele Caci seemed like a really great idea for a meetup talk. The speaker is passionate about both board games and coding, so he decided to implement a proof of concept for the game Ticket to Ride in Go. It wasn’t relevant for me in a conference setting, but I think something similar could be a really nice light talk for a meetup. We do have a [Golang Meetup](https://www.meetup.com/vilnius-golang/events/304548246/?eventOrigin=group_similar_events) in Vilnius. 

### Quotes 

I noted down a few quotes that seemed short and powerful to me. I’m not sure the people came up with them themselves, but I’m adding the people that said it in the conference as the authors.

* “At scale rate problems become common” Russ Cox
* “As programmers we can make our own tools” Qi Xiao - I agree with the speaker that this was more prevalent some time ago and is forgotten too often nowadays
* “Edit & Pray vs Cover & Modify” Federico Paolinelli when speaking about different approaches to changing your code


### Resources 

A few resources I’ve heard about during the conference:



* [Gophercon Europe](https://gophercon.eu/)
* [Fosdem](https://fosdem.org/2025/) + [Config Management Camp ](https://cfp.cfgmgmtcamp.org/2024/cfp)are two free of charge conferences you can visit in Belgium in one go
* [GoTime podcast](https://open.spotify.com/show/2cKdcxETn7jDp7uJCwqmSE)
* [Women Who Go community](https://www.womenwhogo.org/) (Sadly not active in Lithuania)
* [Bluesky Social app](https://bsky.app/) - one of the moderators joked that people are harassing speakers to join Bluesky so they could connect


## Final thoughts

I liked GoLab more than I did [GSAS](https://www.ieva.dev/conferences/gsas_2024.html). However, going to two conferences only a month within each other was a bit too much for me. It took me a while to write this reflection post, because I felt really tired for a few weeks and didn’t have energy for anything after work. I think what drained me so much was also the people aspect. My initial goal for this conference was to connect with the Go developers from my company. In the end I didn’t do that at all. The rhythm of focusing and taking notes during the lectures and being in a really noisy environment during the breaks takes a lot of energy for me. In order to recharge I needed to spend time alone in the evening, but I felt bad about it, as I knew others were going out, having discussions and making connections. 

What are my plans for next year? I would like to choose only one conference to attend per year and to really study the agenda before buying the tickets. 
