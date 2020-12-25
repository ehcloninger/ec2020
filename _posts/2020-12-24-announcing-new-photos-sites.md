---
layout: post
title: "Announcing New Photos Sites"
categories: blog
tags: [2020,web]
---

One of the goals I set for myself when I made this *yet another* iteration of my personal
site was to include photo galleries. I've made progress enough to talk about it.

<!--more-->

In the times before social media made over-sharing possible, we would stick our photos on
whatever photo site met our budget and leave it open to the world. I discovered that wasn't 
the safest option 15 years ago. In 2020, even less so. I'm not willing to share photos of 
my kids or my girlfriend for most of the same reasons that I don't get on Facebook.

For those of you discovering this post from the open internet, you'll find my public photos 
[here](http://photos.ericcloninger.com). There's photos of my car project and some nice 
photography there, but no photos of my family.

If you're a friend or family member, my private photos are available 
[here](http://private.ericcloninger.com). If you want access, just contact me in any of the 
ways you know me and I'll pass along the password.

# The Details

As with my personal site, my photos are using a static site generator and Amazon S3 hosting.
The static hosting aleviates so many security risks. What little need there was for server
work can be offloaded to the viewer as Javascript at the cost of bandwidth. Unlike my work,
I'm not concerned with high SEO on this site. So, some pages may take 5 seconds to properly 
load and that's just alright with me.

If you look at the links and you're a nerd, you'll notice that's HTTP, not HTTPS. With AWS, 
getting SSL to an S3 site involves using CloudFront, which is fine, but CloudFront has a couple 
of hiccups I'm not willing to deal with this week. So, it will stay insecure. This site is still 
on HTTPS, though it really doesn't matter as there's no need for secure interactions.

For the private photos site, I'm using the S3Auth solution that I mentioned in [an earlier post](/blog/2020/12/12/making-this-site-ops-worthy.html#h-staging-site).
The only thing holding that content from the unwashed masses is the strength of the SHA-1 hash,
which is far from perfect. It's not meant to be a foolproof security option, but it's good enough 
to protect what's there from casual observers. Trust me, it's just photos of family outings. 
There's no photos of naked celebrities or Rudy Guliani's secret hair dye formula in there.

# Wrap It Up

It's just after midnight and it's now officially Christmas where I live, so I'm going to sign
off and enjoy the holiday with my family. 

Peace and happiness to you all.