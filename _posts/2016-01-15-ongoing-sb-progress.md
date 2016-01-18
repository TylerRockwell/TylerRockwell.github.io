---
layout: post
title: The Ongoing Smashing Boxes Progress Post
description: "Where I'll write about all the wonderful things SB teaches me"
tags: [career, progress, smashing boxes, learning]
---

So, each entry into this post will follow this format:

* Date
* What did you learn yesterday?
* What are you going to do today?
* What do you expect to learn?

Each entry should be relatively short, but important topics may expand
out into their own posts. We'll see.

## January 15, 2016

### What did you learn yesterday?

Today is day 3 of my Smashing Boxes adventure. Day 1 was orientation,
meeting with the teams, awesome lunch at Dashi, overall just getting situated.
Yesterday was when I first started doing *work*. My first project is to build
a Twitter clone. What makes this more challenging for me is that I must use
Devise for authentication and rspec for testing. I'm getting a handle on rspec.
It's pretty straight forward, it's just a matter of learning the syntax differences
between it and minitest. I spent a lot of time looking over the Devise docs. It's
easy enough to generate a user model and get a working authentication system in,
but everything feels hidden away, so customization has been tricky.

tl;dr: I learned a lot about Devise and rspec.

### What are you going to do today?

So this entry is being done a little late today, so I've already been working on
some things. I got a test that I was struggling with yesterday (Putting to the
update action within the Devise User Registration Controller) working. I updated
my branch to meet the criteria my **awesome** mentor Annie (Hi Annie!) put forth
for me. This afternoon I will work on putting together the user profile page, and
if I have time start working on follower/following capabilities.

tl;dr Keep working on my Twitter clone

### What do you expect to learn?

I expect to continue gaining experience with rspec and Devise. I'm working on my
ability to not just produce working code now, but code that is good as well.

tl;dr It's 2 sentences. Just read it.


## January 18, 2016

### What did you learn yesterday?

I've gotten a bit more comfortable with Devise and how to modify its generated
structures. I'm gettting familiar with rspec syntax.

### What are you going to do today?

This morning I started working with Cucumber. Annie showed me how to write
integration tests with it, and it's already much better than minitest. I'm going
to work on getting my pull requests merged into master and I should finally get
started on the follower functionality. I will also add more integration tests to
make sure that everything I've written thus far continues to work.


### What do you expect to learn?

I expect to learn a lot about proper testing. It (understandably) seems that
testing is very important here, and while I can write tests and make them pass,
there seems to be a long way to go before I have proper DRY and comprehensive
test suites.
