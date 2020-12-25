---
layout: post
title: "Making This Site Ops-Worthy"
subtitle: ""
categories: blog
tags: [2020,web]
---

In the 20+ years that I've owned my name as a domain, I've made many versions of the site
using all kinds of tools. I used some of the early Content Management Systems (CMS) that 
had a lot of security issues. I've built the entire site by hand, using PHP, which had 
hilarious results (/s).

<!--more-->

Since 2014, I've settled on a system called [Jekyll](https://jekyllrb.com) that's used to 
create thousands of Github project pages. Jekyll creates a "static site" that has no
databases or bits of server logic to entice hackers. On the other hand, it allows me to
add new content reasonably easily and make the site look the way I want.

The goal is to make this process as easy as possible without losing performance or giving
up security goals. There's a specialization within Computer Science and the development 
community called *DevOps*. There are lots of subtle aspects to this term, but a site that 
has good Ops can be easily built, tested, maintained, and secured from attackers. Even for
a vanity site like this, those goals are still valid.

### The Problem(s) 

The biggest drawback to Jekyll for me is being able to create content when I want. A 
commercial CMS like WordPress has a login screen and I could create a new blog post on 
my phone while having coffee at Starbucks. With Jekyll, I am constrained to creating
content where I build the site, which is my laptop. Even though I have a nice, powerful
laptop, I'm not always near it when inspiration strikes.

Another drawback of the way I was using Jekyll are the dozens of slightly different ways
between a locally-hosted webserver and one that's operating on the open web. There are
dozens of subtle differences in the built-in webserver that Jekyll uses to host local 
pages and the webservers used on Github Pages or with Amazon S3. I would frequently get
some content looking nice on my local machine and have it completely fail when it went
live. That's always stressful, even if it's just my vanity site.

I've spent a couple hours today working on solutions to both of these problems and I think
I'm close to having a better (but not perfect) solution.

### Amazon AWS Amplify

This site is hosted on AWS, using S3 to deliver a static site. This is a solution used by
thousands of websites. I could've used Github Pages, but I'd like to someday have my 
photos on this site and Github has a site limit of somewhere around 1GB of content. I won't
complain, because they're giving that away for free.

I use AWS for work, so naturally I came here for my personal content. I could've just as
easily used Microsoft Azure and maybe someday I will.

I was serving up content over CloudFront, which provided fast worldwide access to my site as
well as secure access over HTTPS. Both of these are desirable qualities. But, I had to push
content from my local machine after checking the files into my Github repo. I wanted a
solution that would notice when I made to Github checkins, then automatically build and
deploy my website to the hosted space.

**Enter AWS Amplify.**

There are many tools that do automated build, test, and deploy. There are even tools that do 
this over the web and I wouldn't have had much trouble using any of them. The nice thing about
Amplify was how easy it was to connect to my Github repo and set up the build process. I had
to tweak the pre-made config files to add the 3 dependencies that my site had in particular.
This took perhaps an hour to get right.

The next part was figuring out how to get the output to my S3 bucket and into the CloudFront
distribution. That involved at least an hour going down the rabbit hole of Medium blogs, 
StackOverflow questions, and AWS docs (which are a whole different class of rabbit hole). 

I finally realized that I was making it harder than I needed to--I didn't need to worry about
getting my built site into S3--Amplify already creates a container that can be used as
a static webserver. All I had to do was point my DNS entries in Route53 over to the new bucket. 
This new bucket also serves up pages quickly worldwide over HTTPS, so I'm covered.

While, this isn't perfect, I can actually use Github itself to create a file if I wanted from
my phone or someone else's laptop. I could commit those changes in the Github website and merge
into the main branch. Amplify will notice the checkin within seconds. Around 5 minutes later,
the new content is shown on my site. I think the longer-term solution is to get a lightweight
tablet with a keyboard, like a Microsoft Surface or the Samsung Galaxy Tab S7, that I can use to 
create the content and push the changes to github or my staging site.

In case you're curious, it costs roughly $35/year to keep this site going on AWS. $12 of that
is the cost of the domain name renewal.

---
**12/14/2020 Update**: There's a slight bug in the AWS Amplify deploy process. While it worked the
first time, subsequent posts are throwing an error. I've gone back to hosting in S3 until the
issue is resolved, but it's nothing anyone would notice, most likely.

**12/24/2020 Update**: I've bailed on Amplify for the moment and gone back to building and pushing
from my local machine. I have a lot of other projects on my plate and a new role at work that isn't
going to give me spare cycles to track down this issue. Someday...

---

### Staging Site

In these days of Agile projects and continuous deployment, the idea of having "alpha" and "beta"
testing periods are quaint. Some developers (including myself) joke about "testing in production", 
making our users the beta testers. No reputable development team does this. We usually send the 
near-ready code to a "staging" site for automated and human testing. By design, these testing sites 
are as near to the real-world environment as possible. Some of the better web shops can make the 
transition from staging to production in a moments notice.

I don't need that kind of setup, but I do want to make sure my content looks nice in the
real environment before I push it live. Maybe I'll want to show it to someone to make sure 
everything is right before I take it live. That's where my staging site comes in. 

I don't want any of you to see my staging site and access the materials before they're
golden. So, I need a bit of logic for handling a login. However, since my site is static
and has no logic or database, how do I keep your prying eyes out?

The answer is to use [basic-auth](https://tools.ietf.org/html/rfc2617). This has been a trick 
of webservers almost since the beginning. It's not a replacement for a properly-implemented user 
authentication system, but it's more than good enough of for a staging site with my content.

Again, because developers are awesome, there's already a free service to help people like me.
[S3Auth](https://www.s3auth.com/) is operated as a free service by a company that does AWS
development professionally. With just a few small changes to my setup, I can hide my content
until someone manages to break the SHA1 hash that hides the password.

### Calling It A Day

I started messing with the deploy tool yesterday evening after work and continued for about 
an hour this morning. Then, my girlfriend and I did some shopping in OKC and ate Korean Fried 
Chicken. I came home late in the afternoon and spent a couple hours finishing up the webserver 
changes and trying out the staging site.

I realized that I spent more time writing this up than I did implementing the staging site.
Hopefully, when this gets indexed by Google, the next person might get the benefit of my 
learning and it makes their life a little easier. Sorry, future human, I can't write shorter
sentences.