---
title: 'Learning Chef'
subtitle: A Guide to Configuration Management and Automation
author:  Mischa Taylor, Seth Vargo
rating: 3
date: 2024-09-15
goodreads_link: https://www.goodreads.com/book/show/19485033-learning-chef
---

**Why I read this book:** Recently I moved to the role of Site Reliability Engineer (SRE) and Chef is one of the tools SREs at our company use heavily. I’ve decided it is a good place to start learning.

**How I read this book:** I’ve read a PDF version while trying out every exercise described.

**What I liked about it**: 

The chapters were short enough so I could go through a single chapter in one sitting (~ an hour).

The contents of the book seem to be well thought through - it covers all the basics concepts of Chef, what you would need to do to use Chef in your infrastructure and even some Ruby basics. In this regard this is still a good resource to gain basic understanding of Chef.

Since I was doing a lot of copy pasting of little yaml and JSON files for the exercises, I’ve turned it into an opportunity to improve my Vim skills and googled things like the shortcut for deleting the entire line. 

The chapters that seemed most useful for me:
* **Chapter 8: attributes**. Mostly for the ​​priority scheme for how attribute values are composed from multiple sources
* **Chapter 11: Chef zero.** Because it gives an overview of how managing your infrastructure with Chef looks like and the ability to explore that locally.

**What I disliked:**

The biggest issue with this book is that it is already outdated. It was released in 2014 - ten years prior to when I started reading it. The most notable change is that the resources that were supposed to be online to get through the exercises easier are no longer there. Chef itself has also moved forward e.g. the book talks about chef DK, but the current solution is actually Chef Workstation. ServerSpec seems to have also been [replaced](https://www.chef.io/blog/the-road-to-inspec) by InSpec. Foodcritic was replaced by Cookstyle. Having said that, with a little bit of googling I was still able to achieve what the exercises required.

In the final chapters of the book I’ve started to notice some discrepancies e.g. exercises describing creating a ‘webserver’ role and later you are required to use ‘webmaster’ role. It felt like these final chapters didn’t get as thorough a review as the initial ones did.

At first I had issues with Ruby dependencies breaking every time I tried to test something. But then I came upon this [comment](https://github.com/test-kitchen/test-kitchen/issues/1090#issuecomment-235911674) saying `If you are not using the ruby bundled with chef-dk its "swim at your own risk"`. After I’ve set up the ruby environment based on[ this guide,](https://docs.chef.io/workstation/getting_started/#configure-ruby-environment) I haven’t experienced any more problems.
