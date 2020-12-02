---
layout: about
title: About
---

## About Me

I'm a software developer and product/project manager at Samsung Electronics. My CV is on
[LinkedIn](https://www.linkedin.com/in/ericcloninger/).

I live in a small town in western Oklahoma and I've worked from home for 20+ years. Before
the COVID pandemic, I frequently traveled as part of my work.

## About This Site

This site is hosted on Amazon S3, which typically costs me less than $2.00 per month for 
the hosting, including the domain name and the SSL certificate. I recently switched from using 
Atom to VS Code and I'm finding myself working more on my projects than spending time to get my 
environment to do what I need. Since I'm a bit old-school, I tend to work in the Bash shell most 
of the time, using Ubuntu 18LTS under the Windows Subsystem for Linux (WSL).

I based this site on an existing theme that uses devOps principles to specify all the dependencies
rather than installing them manually. I'm trying to get to an easier process that requires fewer 
bash scripts and help to get published. Ideally, it should be possible to clone my repo and use 
`bundle install` to get all the dependent packages needed to build.

Now, I can simply use `jekyll build` to create my site and `s3cmd sync` to deploy to S3. I'm still 
trying to find a better way to create image galleries as that's going to be a frequent use for me. 
I'd love to have an image gallery component that works in Jekyll that doesn't require the images be 
within the Jekyll folder structure. That way, I could put my images in a separate S3 bucket and use 
CloudFront to propagate them.

## Copyrights

All photographs on this site, used in the banners and shown in image galleries, are original
works by Eric H. Cloninger unless otherwise credited. All rights are reserved.

## Credits

* This site is powered by [Jekyll](https://jekyllrb.com/).
* The site design is based on [Yat, yet another theme](https://github.com/jeffreytse/jekyll-theme-yat), by [Jeffrey Tse](https://github.com/jeffreytse).
* Image gallery is from [jekyll-image-gallery-example](https://opieters.github.io/jekyll-image-gallery-example) by Olivier Pieters
* Icons on this site are provided by [Font Awesome](https://fontawesome.com/).
