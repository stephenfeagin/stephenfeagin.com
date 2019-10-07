---
title: "Projects"
date: 2019-09-21T14:48:03-04:00
draft: false
---

This page will serve as an index of side projects that I'm working on, and maybe some that I would
like to try but haven't started yet.

## Blog Comments

I am building a web service using Go to add commenting functionality to this static site. I plan to
use standard library Go as much as possible for the backend, though will probably use a third-party
servemux to implement URL parameters. I plan to deploy it as a REST API onto Heroku. 

I want to create a basic admin frontend that only I will have access to, where I can review
comments, delete them, update them, etc. This will require database query functions, user
authentication, and some basic HTML forms and templates.

The main functionality will be to serve as a REST API for the static site to call using
AJAX/JavaScript fetch. This will involve database query functions and JSON marshalling on the
backend, as well as HTML, CSS, and Javascript on the frontend Hugo site to display the comments. The
frontend matter will be implemented as a Hugo template partial to be included in the post/page
templates.

In the future, I may build in integration with [Akismet](https://akismet.com) spam detection. That
would definitely be more involved, and require adding user login for the comments in addition to
coding up the API functionality.

## Personal Finance Tracker

Django web app to log and display financial transactions and keep track of account balances and
budgets. I've had a few false starts on this project, I think because I didn't take the time to
break it down into smaller manageable chunks from the beginning. I'll write about the overall plan
and structure for this project soon, and put up some posts about the work itself.
