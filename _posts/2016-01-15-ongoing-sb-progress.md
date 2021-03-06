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



## January 27, 2016

### What did you learn yesterday?

Yesterday, I did the Gilded Rose kata. I got some great experience in refactoring
code that isn't structured well, and learned some about how much easier it is to
add features into a program once it broken down into easy to understand parts. I
got a little more familiar with collection_select fields as well.

### What are you going to do today?

Today, I'm going to try my hand at the Gilded Rose kata without refactoring the
original code. I'm curious to see how much effort it takes. I'm assuming it will
make the jumble of if statements even more complicated and harder to maintain.

After that, I'll be working on the Rails Bookstore app. I've got the books model
and controller in place, and the books are sortable by any field on the index
(although it's currently not done the best way). I'll likely implement user/admin
accounts today as well.

### What do you expect to learn?

I'll be using devise to handle the user/admin accounts. I'm expecting to learn
how to properly manage the different account types and control their access to
different parts of the site.

## January 26, 2016

### What did you learn yesterday?

Yesterday, I learned about iTerm2 and zsh. I had heard of them previously, but
had not used them. I'm now running oh-my-zsh with the candy theme. I'm probably not
using all of its potential yet, but it is nice to have branch and ruby information
right in my prompt.

I also spent some time at the end of the day yesterday writing controller tests
for the ToDo API. From that, I learned testing JSON is tedious. It's easy to have
tiny discrepancies that cause the tests to fail. Like most things, I'm sure it'll
get easier with time, but not quite yet.

### What are you going to do today?

Today, I'm finishing up tests for the ToDo API. I'll likely be starting on the
Rails Bookstore, which is the last major project of the apprenticeship. I expect
that to take some time, so that's likely what I'll be doing for the next several
days.

### What do you expect to learn?

I expect to learn some more about testing JSON and an API in general.


## January 25, 2016

### What did you learn yesterday?

These are always the worst to write on Monday. Friday, I learned a bit more
about the proper place to put new actions and that it's okay to make an extra
controller with only a couple actions for the sake of organization.

### What are you going to do today?

Today I'm finishing with the Twitter clone. (How many times have I told myself
this already?) Anyway, I just need to finish refactoring to better, more RESTful
routes. After that, I'll be working some more on the Rails Refactor project, and
possibly on the Rails To-Do API as well.


### What do you expect to learn?

I'm expecting to learn more about getting data to views without violating mvc flow
and also without having several instance variables in the controller. (Sandi Metz
says more than 1 is too many.)


## January 22, 2016

### What did you learn yesterday?

Yesterday I learned about decorators and Draper. Essentially, decorators allow you to clean up your views by removing logic from them without cluttering up your model with methods that just format output. Since those methods don't really fit in either place, Draper provides a wrapper class to the model that is called by appending `.decorate` on the end of instance variable assignments. e.g. `@user = User.find(params[:id]).decorate`. Very cool.

### What are you going to do today?

I need to get in the habit of writing these posts earlier. Today I have worked on getting a bio and picture ready for smashingboxes.com. I spent some time this morning trying to think of a better way to make the roman numerals kata, but beyond moving the conversion hash into an instance variable, I came up short. This afternoon, I'll be working on the API for the todo app and pairing with Annie on a project.


### What do you expect to learn?

It's been a little bit since I built an api, so I expect to get a refresher on jBuilder. I'll likely also learn about writing integration tests for api's. I don't know what Annie and I will be working on, but whatever it is, I'm sure I'll gain some valuable knowledge from her as well.

## January 21, 2016

### What did you learn yesterday?

Yesterday, I spent some time working in vim. I used it for my morning kata, and
also for editing the nginx config file on Digital Ocean. I feel slightly more
comfortable with it. I've gone from not being able to edit text at all with it
and desperately typing :q every time I open it, to being able to write what I need
at painfully slow speeds. That's an improvement, right? I learned a bit about
nginx itself. The ssh portion was familiar, but editing the nginx config file was
new to me.

### What are you going to do today?

Today, I'm working on getting my environment set up to run the ember portion of
the to-do app. Assuming that goes well, I'll likely start building the API for it
today. I believe I have some code review comments to address for the Twitter clone,
so I'll also need to incorporate any recommended changes into that.


### What do you expect to learn?

I'm going to do my katas in vim from here on out, so I'll get more practice with
that. Yesterday ended with npm vanishing as a command in my terminal, so perhaps
I'll figure out why that happened. I'm sure there are nuances of code development
that I'll learn today as well. It seems like every day I learn at least a few new
things that I could not have predicted in this blog.

## January 20, 2016

### What did you learn yesterday?

As I mentioned yesterday, I learned quite a bit about tests and fixtures. I've
gotten a bit better with integration tests. I went from feeling like I was just
getting tests to run and pass through shear luck to feeling like I am ready to
work on improving my test writing style to better meet best practices at SB.

### What are you going to do today?

Today, I'm going to set up the nginx server on Digital Ocean. This needs to be
done using vim, so in preparation for that, I wrote my code kata entirely in vim
this morning. Using vim at the moment sort of feels like trying to run a marathon
with my legs on backwards. I can see where I need to go, but getting there is slow
and cumbersome.


### What do you expect to learn?

I expect to learn some about containers, ssh, vim, and setting up a web server.
So, it seems like today will be a lot of devops type of work. While some developers
shy away from things that aren't strictly development, I think it's important
to understand the whole environment I'm working in. I don't think I need to master
every aspect right away, but at the very least nothing should feel like it's just
done by magic.

## January 19, 2016

### What did you learn yesterday?

I learned the basics of Cucumber. I like the feature files, and the steps aren't
all that hard to write either. I got follower functionality up and running yesterday,
but I feel like I understand only about 80% of it. I should be able to use what
I've learned to get the ability to favorite posts up today.

### What are you going to do today?

I'm going to write more comprehensive tests, primarily model tests, but also more
integration tests since I no longer hate them. Annie helped me understand how Cucumber,
rspec, and FactoryGirl all work together. Test writing can be time consuming, but
I know how important they are, so I'm determined to get good at writing them. I
should be able to finish the Twitter clone project today.


### What do you expect to learn?

I expect to learn more about testing best practices. My talk with Annie this morning
helped me to understand all the different pieces of the tests. Tomorrow I plan
to start on the task of setting up nginx on Deep Ocean, so I'm sure I'll learn
a lot about that tomorrow.

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
