---
title: High Performance Browser Networking 
author:  Ilya Grigorik
rating: 5
date: 2021-11-12
goodreads_link: https://www.goodreads.com/book/show/17985198-high-performance-browser-networking
---

__Why I read it:__ Few colleagues praised the book as a very useful read.

__Short Summary:__ 

![Network stack](/assets/images/hpbn.drawio.svg){: width="375" }

The book goes through most layers of the network stack (picture above) with great detail, explaining (in the following order) TCP, UPD, TLS, how WiFI and mobile networks work, HTTP and various browser APIs. The author's idea is to really explain the working principles of these technologies and then use that deep understanding to suggest performance optimizations. Each chapter builds on previous ones and reiterates some ideas helping to understand and memorize things even better.

__What I liked about it:__ 
I was pleasantly surprised how much I liked the book. One of the people who recommended it to me said it was 'very useful but also a difficult read'. But for me it somehow connected my interest in reading non fiction books for the sake of understanding the world better and the wish to learn new things in order to be more efficient at work. For example, author explained very well how mobile networks work - what all the generations mean, how the data travels from some server through mobile signal towers all the way to your phone (just a general interesting thing) and how each of the components of mobile networks contributes to the latency of the signal and how the network traffic should be optimized to save battery life (might come in handy some day at work).

From time to time I attempt understanding how the internet works - google something, watch a documentary, read a technical blog post. But I never came across a resource that would explain it in a way that would really stick. Until I found this book. The way how author explains things, how he goes through entire network stack and how each part builds on another really worked for me. I'm sure I won't be able to remember all of it after awhile, but it will be very easy to get back to the book for a quick reference as a lot of things (like TCP and TLS handshakes) were also visualized in a very clear way.

__What I disliked:__
The book is a little outdated. The version I had says the newest edition was released in 2015 and the cover proudly brags about it being updated for HTTP/2. But we are already at 5G and HTTP/3. 

There were two sides to the book: explaining in detail how different technologies/ protocols work and providing tips on how to optimise them for better performance. Since I wasn't very familiar with a lot of things explained in the book, I focused solely on understanding the basics and skimmed the performance optimization parts a little (especially those concerning some configurations on the server) as it felt like to much information in the moment. Though suppose I might get back to those specific chapters later.

Not all chapters were equally interesting. Once I got the last part 'Browser APIs and Protocols' discussing things like WebSocket and WebRTC I noticed my reading got slower and slower and I really struggled to get through it. 

__Quote:__ No bit is faster than a bit not sent!