---
title: 'Side quest: Setting up CDN'
---

I have a confession to make: I am always a bit reluctant to post content on LinkedIn. I feel like the social network 
is currently going through a phase Facebook has gone through several years ago: people eagerly oversharing. And I'm not sure if I want to be a part of that. But I end up posting anyway justifying myself that it is mostly professional content. And doing so turned out to be a good thing. 

Our (Vinted) Platform team lead noticed my post about learning infrastructure things via hosting this blog
and suggested to collaborate on a presentation about Content Delivery Networks (CDN) he was doing for an internal learning session. He would use my website for the demo and I'll get to learn new things. I was also interested in the topic as Udi Dahan mentioned CDNs as part of strategies for performance optimization in the last part of his [Advanced Distributed Systems Design course](/reviews/udi_dahan_adsd.html).

### What's a CDN?

There are a lot of great [answers](https://www.cloudflare.com/en-gb/learning/cdn/what-is-a-cdn/) to this question on the internet. But for the sake of easier flow of the text in this post I will provide a short answer as well. 

![Tiers](/assets/images/cdn_tiers.drawio.svg){: width="500" }

A CDN is a geographically distributed group of servers. If CDN is allowed to cache the response it can serve it to the user right away, without going to the origin server at all. This helps to reduce distance between users and website resources.

### The demo

The idea my colleague had was to add this blog to Cloudflare and run a load test requesting an image asset from it while monitoring the response times. To show the effect a CDN has on website's performance he wanted to toggle different parameters:

- __CDN ON/OFF__ - changing whether a Cloudflare IP address or that of the origin server will be resolved by DNS lookup. When Cloudflare is allowed to proxy the requests and responses it can also cache some assets for better performance. The caching can be configured both in the Cloudflare UI or on the origin server. The later is done via [Cache-Control headers](https://developers.cloudflare.com/cache/about/cache-control). And that was the second parameter changed in the load test. 

- __Cache Control headers on the origin server:__
    - `no-store` -  any cache (i.e., a client or proxy cache) must not store any part of either the immediate request or response;
    - `no-cache` - the response can be stored in caches, but must be validated with the origin server before each reuse;
    - `private` - the response message is intended for a single user (e.g. a browser cache) and must only be stored by it;
    - `public` - any cache may store the response.

Since my website is hosted in AWS eur-west-1 zone (Ireland) colleague ran the test from Toronto - to provide more distance between client and server and hence a more visible latency. 

### What did I have to do?

__Transfer DNS zone to Cloudflare.__ This entails creating a Cloudflare account (free for personal or hobby projects), configuring the DNS records there to point to the AWS setup where the website is running and finally updating nameservers at the domain registrar to the Cloudflare ones.

This was super easy as Cloudflare's UI is well thought through. It recognized the registrar I use and showed me instructions for what I need to do there. It also tried to resolve the needed DNS records for me. But there was a small catch. I have a load balancer in front of my instance to allow for easy instance replacement. The resolved DNS configuration had an A record with load balancer IP. But these IPs are actually constantly changing - what I needed instead was CNAME record with my load balancer DNS name.

__Add Cache Control headers to the server.__ I needed to be be able to change the Cache-Control headers sent by the origin (my AWS instance). Since I use nginx to run the website, I basically needed to add these two lines to the website's config file:

```
expires 5m;
add_header Cache-Control "public";
```

and then update with specific header value when needed. 

Every time I updated the configuration file I checked if it is ok using `nginx -t` command and then reload nginx using `nginx -s reload` command for the changes to take effect.

### Reflections

__Seeing network basics in action.__ Recently I finished reading ['High Performance Browser Networking'](/book_reviews/high_performance_browser_networking.html) book which detailed the different steps (TCP, TLS handshakes, actual data transfer) involved in communicating over the network. It helped me a lot when it came to visualizing what is happening during the load test.

Tests results for response latency obtained by running load test while trying out different CDN and cache control settings looked something like this. 

![Latency graph](/assets/images/cdn_latency.drawio.svg){: width="700" }

As we can see:
- When there is no CDN involved the latency is very high.
- Once the CDN is enabled (and allowed to cache the response as there are no headers specifying otherwise) the latency drops significantly.
- If the CDN is allowed to proxy the requests but not to cache the result the latency rises but just a little compared to the CDN OFF case.
- There's not really any difference between no-cache, no-store and private Cache-Control headers.

Why is that?

![Latency graph](/assets/images/cdn_tiers_tcp.drawio.svg){: width="700" }

Any request-response communication over HTTP connection includes a TCP handshake before the actual data transfer. So we have one round trip for the handshake and (at least) one for the actual data transfer. The duration of these roundtrips depends on the distance between the requestor and the server. And as mentioned before that is exactly the distance CDNs help to reduce. If CDN is able to handle both the handshake and the response serving, the roundtrips will be very short. And even if it is not allowed to cache (all three `no-cache`, `no-store`, `private` headers) the response we save some time on the handshake roundtrip. CDN keeps a connection to the origin server at all times, so an extra handshake is not needed there. 

__Collaborating with someone outside the team.__ I always appreciate a chance to work or otherwise collaborate with people outside my team. As it may make future collaborations easier. When I need something work related from another team it is much easier to go and ask them, if I already know somebody there. And sometimes that might be just the right encouragement needed to prevent trying to figure things on my own. Which can lead to a worse or at least slower result. 

And of course there's also the added benefit of learning new things from new people. For example by observing their ways of doing stuff that I can try and adapt later. One of such thing was evaluation of tools chosen for a task. 
The initial setup for the load test was [BetterUptime](https://betteruptime.com) to monitor the request latency to this blog, as seen from different regions of the world and [Vegeta](https://github.com/tsenart/vegeta) HTTP load testing tool. But they didn't seem to provide enough flexibility for my colleague so he moved on to the combination of [Prometheus blackbox exporter](https://github.com/prometheus/blackbox_exporter) and [k6 load testing tool](https://k6.io/). 
I think the approach of starting simple, understanding the limitations of the tools and moving to something that suits your goal better is very neat. 


### Did I tear it down after?
I torn down the initial BetterUptime monitoring setup. But I left the Cloudflare since it is free. It is nice that all these tools have free plans for learning and hobby purposes. 