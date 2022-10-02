---
title:  'Short update: Moving the blog from AWS to Github Pages'
---

I launched this blog [last year on AWS](/2021/09/12/how_this_site_came_to_be.html). It was my first time using AWS so I was eligible for the Free Tier services. Running my blog cost me around $2 monthly. However, by the end of this August my AWS Free Tier expired and the expenses of running the blog rose to around $35. One third of it was for a single Linux t2.micro instance and two thirds - for the Load Balancer. 

I had plans for using AWS to play around with different deployment setups e.g. using Docker and Kubernetes. But at the moment I have other priorities after work, so I know I won’t be able to assign much time to this and will be paying around $420 a year just for keeping the blog around. 

The blog is set up with [Jekyll](https://jekyllrb.com/) and I already had experience with hosting a static site made with [Jekyll on Github Pages](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll), so I decided to transfer my blog there for now.  It was super easy to do - mostly I just needed to rename the repository,  add a github pages gem to the project and reconfigure DNS. 

## Were there any options for reducing the price on AWS?

I could have gotten rid of the Load Balancer as it consistutes the biggest part of the costs. However, that would require investing more time into figuring out how to make sure that after I deploy changes to my blog and a new server instance is spun up, my DNS setup on cloudflare points to it. 

I discussed this briefly with the friend who mentored me through the initial setup and he suggested these options:

* Looking into Cloudflare API to see if there is a way to update the DNS records within the deployment script;
* Seeing if there is a way to buy IP addresses on AWS and then assign them to the instance created via deployment.

Both of these sound interesting from the perspective of trying something new, but they would have required a lot more time/ effort and I would still have to spend a bit over $100 a year just keeping the blog up. 

## Do I still plan to learn more about different deployment/ infrastructure technologies? 

I really hope so. I’ve seen some [tutorials](https://talk.jekyllrb.com/t/new-video-develop-jekyll-or-github-pages-using-docker-containers/7199) for developing Jekyll blog and Github Pages on a Docker container. I assume this would be less challenging then setting up an environment for the AWS instance with Nginx. But it still would be a start and a good opportunity to motivate myself to read Docker documentation. 

As for Kubernetes, I recently bought the book [Kubernetes: Up & Running](https://www.goodreads.com/book/show/60888727-kubernetes) and I’m considering it to be my next technical read. I would like to start learning more by tinkering around, but learning by reading is still very much my comfort zone.