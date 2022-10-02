---
title: CQRS, DDD, EventSourcing course
author: Greg Young
date: 2019-07-15
---

**Disclaimer:** This review is written a bit more than 2 years after watching the course. It is based on the notes I made while watching it.
### General impression
I got the videos of the course from a colleague. I'm not even entirely sure what is the official name of the course. In the introduction Greg Young says it is based on his 3-day workshop on CQRS, DDD and EventSourcing. The content of the videos was a little scattered even though I watched them based on their numbering. Some videos only showed Greg talking next to a whiteboard and some were probably filmed at the said workshops.

Despite of the chaotic nature of the contents, I liked the course a lot. It was very practical and hands on. Instead of going into an abstract theory of things, Greg gave practical advice and pointed out common issues. Plus a lot of what he was talking about was very similar to the architecture I was working with at the time, so it was very nice to have those practical examples in my mind while listening. It helped me to understand why the architecture was modeled the way it was.

Having said that, this was not a course for someone looking to get introduced to DDD or finding out how to build a correct domain model. It was focusing more on the infrastructural elements of DDD + CQRS + Event-Sourced architecture and common pitfalls. 

### Contents of the course
- When to DDD?
- Bounded Contexts and how to find their boundaries
- What are application services/ command handlers?
- Projections/ Views/ Read Models
- EventSourcing (and modeling event sourced Aggregates)
- Event versioning
- Testing
- Pull vs push models (request-response vs publish-subscribe)
- Process managers/ sagas
- Deferred message alarm clocks
- Going into some specific use cases (e.g. dynamic content type negotiation across event-streams, CQRS for occasionally connected systems)

### Ideas I liked the most

Ideas I found the most interesting/ useful based on my experience or just want to have here for quick reference.

#### When to DDD?

Let's say we are estimating in shirt sizes S(mall), M(edium), L(arge) the business value and technical complexity of a service, then:

| Business Value | Technical Complexity | Tips on building it         |
|      :---:     |         :---:        |       :---:                 |
|        S       |           L          |       Buy it                |
|        L       |           L          |     **Apply DDD here**      |
|        S       |           S          |     Train junior devs here  |

#### What are application services/ command handlers?

The terms application services and command handlers can be used as synonyms as both of their jobs are:
- Coordinating domain objects (getting the right objects from the repositories and passing them around)
- Bringing in the dependencies
- Transaction management
- Permission handling
- Logging 

#### EventSourcing: storing structured model vs event source (event-log)

We are thought to focus on the structure of state. But state tends to change over time. Plus systems can reach the same state in different ways. All this information is lost if we only store the final structure of state.

Event sourcing, on the other hand, says all state is transient and you only store facts. Any state that we have we derive by *replaying* these facts. We can derive infinite number of structural models this way.

#### EventSourcing and Aggregates

There is no connection between Aggregates and event sourcing. We can store Aggregates in non-event sourced way. We can publish events directly from command handlers.

But in case we want to combine these two approaches, there are 2 important rules to remember:
- Event methods are **not** allowed to do behavior, but are allowed to mutate state.
- Public Aggregate's methods are allowed to do behavior (calculations, validations etc.), but are **not** allowed to mutate state.

If we do not follow these rules event replays can break or we can end up not having the full state after replay, as part of it is set in public methods.

Here is a code snippet to illustrate the different method types more:

```
    public class SomeAggregate : BaseAggregateRoot
    {
        ...

        public void SomeMethod(SomeCommand command)
        {
            // validations
            // calculations
            
            var methodAppliedEvent = new SomeMethodAppliedEvent();
            Publish(methodAppliedEvent)
        }

        ...

        private void When(SomeMethodAppliedEvent event)
        {
            //mutates state
        }
    }
```

And what state should be stored on the Aggregate in the event method? Only the state you need for validations or calculations in your public methods. All the other state can just be stored in the events. 

#### Event versioning
- Never make a destructive change (removing or renaming a property) to an event without making a new event version;
- Upcast all events to the newest version when reading from repository and before passing them to Aggregate;
- Old version of event must be convertable to the new version. If not, you have a new event and not a new event version;
- Consumers need to be upgraded to listen to new even versions before you start publishing them;
- Don't change semantic meaning (e.g. measurement units) when versioning.

#### Process managers | workflows | orchestrations | sagas

All of the above words are meant to describe code that manages life-cycles. That could often involve integration of multiple Bounded Contexts. There shouldn't be a lot of business logic in process managers, just *process* logic that could be expressed by sending and receiving messages.

#### Deferred message alarm clocks

Process managers often need to deal with time (e.g. if I don't hear from billing in 5 minutes, I need to escalate). But it is easier to deal with (and test) messages than clocks. So alarm clocks can be implemented via deferred message service. That is a service that will return a message you sent to it after specified interval of time.

Implementing alarm clock via deferred messages has an additional benefit of being able to store state in the message and minimize the state stored on the process manager itself.

Some tips:
- You don't need to cancel your messages to the alarm clock service, simple drop them if what needed to happen happened;
- If you're sending a message for something to be done also send a message to alarm clock service to wake you up - don't let the process stay in zombie state.

#### Practical slogans

- **Don't try to solve all problems in code** - some problems can be solved by re-negotiating requirements and consistency boundaries
- **Don't automate every single use case** - for low frequency problems an email with manual handling instructions is quite enough
- **Always doing same thing is stupid** - DDD or messaging are not silver bullet solutions that should be applied to *all* the services. 