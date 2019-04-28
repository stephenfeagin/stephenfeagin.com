---
title: "Pelican Rmd Reader"
author: ""
type: ""
date: 2019-04-28T12:51:38-04:00
subtitle: ""
image: ""
tags: []
draft: true
---

I first looked into [Pelican](https://docs.getpelican.com) because I'd
used it a little bit before, it's written in Python so I could potentially extend it myself, and
because it had a plugin to deal with R Markdown documents. When I started importing old blog posts,
I found that the **rmd_reader** plugin was broken -- I was getting an error from the **rpy2** package
when I tried to build the blog with a `.Rmd` file. I did some digging, and the plugin does not
support **rpy2** 3.0 or later. That's a pretty recent release, so I opened an issue on GitHub and
figured I could probably patch it myself. After looking through the internals of **rmd_reader**, 
**rpy2**, and the R package **knitr**, it looks like the fix is pretty easy. However, the process of
trying to work with the R interface for Pelican turned me off to the idea
