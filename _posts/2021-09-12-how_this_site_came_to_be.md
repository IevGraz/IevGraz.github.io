---
title: How this site came to be
---

Some time ago I've been talking with a DevOps oriented friend that I feel bad about my lack of experience with lower level, more technical aspects of Software Engineering (like actually deploying an application to a server instead of just clicking a button in a CI/CD platform configured by someone else). He suggested to help and guide me through the process if I can come up with a project for myself. 

The idea lay dormant for a while, until I decided I want to start posting my technical book reviews (that I was writing on GoodReads for a few years now) to LinkedIn, to be able to share them with my colleagues. I didn't like the LinkedIn article writing UX and the fact that the posts end up being scattered and it is hard to just provide a link to someone 'hey, these are the books that I found interesting'. And it made me think this could actually be a nice opportunity to get acquainted with the aspects of Software Engineering that I don't experience in my day to day work - fronted development and deployment.

### Frontend

I've built the site with [Jekyll](https://jekyllrb.com/). Instead of using an existing theme I decided to spend time understanding how it works and building something myself. That went quite well with the structuring of the site, but when it came to the actual looks I mostly just mashed two themes together: [Jekyll Hyde Theme](https://jekyllthemes.io/theme/hyde) and [a simple cards based template](https://jekyllthemes.dev/a-simple-jekyll-template-card-based/) by copy pasting bits of CSS. 

### Deployment

This is where the help of my friend came in. We decided to deploy the site to AWS as this is something widely used in the industry and worth having experience with. And I haven't had AWS account before, so I am still eligible for the AWS free tier 12-Months Free offer. 

Amazon provides [S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html) for static websites hosting, but we thought that would not be a sufficient learning experience for and chose to host the site on [EC2](https://aws.amazon.com/ec2/?ec2-whats-new.sort-by=item.additionalFields.postDateTime&ec2-whats-new.sort-order=desc). 

My friend turned out to be an extremely structured professional and detailed each step of the process in GitHub issues on the repository containing the Jekyll code of this site. Each issue built on a previous one, to help me understand the usefulness of various features. The issues I've closed already to launch the initial version of the site contained:

- Setup of the AWS account.
- Running an EC2 instance and SSH to it.
- Deploying the website by simply SCP'ing the files from my laptop to the EC2 instance and launching nginx to serve web request.
- Creating an Amazon Machine Image (AMI) from the instance I launched, to preserve the data and make launches of new instances in case of crash or termination easier.
- Setting up EC2 Auto Scaling to make sure my website is always available (or almost always available, as I decided it is sufficient to keep only 1 instance running).
- Creating a load balancer to avoid needing to copy a new DNS address every time a new instance is launched.
- Setting up DNS to use the ieva.dev domain I bought a while ago.
- Setting up TLS certificate to be able to serve HTTPS requests.

### What's next

I was very excited to launch the website as soon as possible, so decided to do it after the above described simple steps were done. But I also enjoyed the guided learning experience immensely, so I'm planning to try out a couple more things like setting up GitHub actions to make adding new posts to the website easier, containerization, launching new version of the site without downtime etc. And share the experience here in a new post!