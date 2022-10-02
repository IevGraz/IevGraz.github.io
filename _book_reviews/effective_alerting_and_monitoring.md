---
title: Effective Monitoring and Alerting
subtitle: For Web Operations 
author: Slawek Ligus
rating: 3
date: 2020-02-02
goodreads_link: https://www.goodreads.com/book/show/16043274-effective-monitoring-and-alerting
---


__Why I read it:__ Wanted to improve the alerting and monitoring setup at work and was looking for books about it.

__What I liked about it:__ That it gives some practical, actionable tips e.g. on plotting and understanding graphs (the typical quantities metrics represent, summary statistics best fit for those quantities), setting up alerts, calculating thresholds. Also I think this book really shows how mature monitoring culture should look like: monitor extensively – alert selectively. 

__What I disliked:__ The author is a devops so naturally the book is written from devops perspective, most examples are about CPU usage and etc. I as a developer would be more happy with application monitoring examples. Plus the language was more complex than it needed to be, as I mentioned before.

__Quotes:__ “Monitor extensively and alert selectively: identify what metrics drive your business and work top-down to setup alarms around timeseries behind KPIs”

“Ideally, monitoring should enable operators to drill down from high level overview into the fine levels of details, granular enough to point at specifics”

“Flawed assumption: the ticket generated from an alert is a unit of work rather than an indication of a problem in the system”

“All alarms that trigger on non-issue should be done away if there is no evidence that the resulting alerts are actionable. If this policy is not followed, false alarms will cause more harm than good. There are only 2 ways one can respond to non-issues: ignore it or overreact”

“Measuring quality most not be effort-full, otherwise quality assessment will come at a very high cost and with dubious credibility”