---
title: "Hugo Workflow"
author: ""
type: ""
date: 2019-04-28T12:15:54-04:00
subtitle: ""
image: ""
tags: [hugo, make, r, rmarkdown, workflow]
---

I recently ported my pretty defunct blog over to Hugo, after some considerable searching about the
best option for my needs. I wanted to be able to work with R Markdown files, but not have to mess
too much with the internals. I had messed around with 
[Blogdown](https://bookdown.org/yihui/blogdown/) a couple years ago, and thought it may be a good
starting place. The issue is that I don't want to have to work in RStudio for all of my website 
work. I have some R Markdown files, but I doubt it's going to be a huge part of the blog, and I
would prefer to use a different editor.

After poking around a bit into Blogdown and [Hugo](https://gohugo.io), I came to a nice workflow.
I only need to run the Blogdown functions when I need to render a new R Markdown file, and I can use
the native Hugo commands from the terminal or whatever editor I'm using. So I made a really simple
Makefile for the different tasks I may need to run:

{{<highlight make "linenos=table">}}
.PHONY: build-and-serve clean-public rmd rmd-serve
PUBLIC_DIR = public

build-and-serve:
	hugo && hugo server

rmd: 
	Rscript -e "blogdown::build_site()"

rmd-serve: rmd
	hugo server

clean-public:
	rm -rf $(PUBLIC_DIR)
{{</highlight>}}

I can continue to just use `hugo` to quickly build the site, but I added a command for 
`build-and-serve` to automatically launch the local server. I've got an `rmd` command to run the
R code to render the `.Rmd` files into HTML and build the site (it calls `hugo` internally, so I 
don't have to include that as a separate command). And I made an `rmd-serve` command to render the
file and run the server.

It's a really simple, pretty blunt tool, but it's really helpful. And it's my first time really
working with Makefiles, so it's a nice, easy introduction.

In the future I'll probably add a command to deploy the site as well, but it's easy enough to just
do it through git for now.
