---
layout: post
title: The Ongoing Smashing Boxes Progress Post March 2016
description: "Where I'll write about all the wonderful things SB teaches me"
tags: [career, progress, smashing boxes, learning]
---

## March 11, 2016

### What did you learn yesterday?

I spent the majority of my day pairing with Patrick yesterday. As we worked through adding relatively
common features to the project he's working on, the benefits of pair programming started to become clear.

With each of us contributing our ideas, we were able to come to better design decisions more quickly by working
together. Features were implemented faster, and we didn't get hung up on one thing for too long even
when issues inevitably came up.

### What are you going to do today?

Today, I'm trying to improve my skills with javascript websites, and dissecting how they work using
the Chrome developer tools. I'll be taking some time to learn about NodeJS, as I will likely be
working with that soon.

### What do you expect to learn?

I expect to learn how to do something in Node. At this point I've never used it (besides the few hours
that I paired with Jordan), so anything will be an improvement on where I'm at now.

## March 10, 2016

### What did you learn yesterday?

Yesterday, I learned some more about Android development. I paired with Nick, and we implemented some view
handlers, and made a few small UI improvements. I may not be ready to build production level apps,
but I've at least got an idea of what Android development is like.

### What are you going to do today?

Today is the last day of my pairing tour, and I'll be pairing with Patrick. I'll be sure to update
tomorrow about what we worked on. Aside from that, I'll be looking into working with the Mechanize
gem today, and possibly swap my scraper to downloading a CSV file and parsing data from that, which
would speed it up substantially.

### What do you expect to learn?

I'm sure most of whatever Patrick and I cover will be new. Using Mechanize will be new to me, and
while I've parsed CSV data before, it's not something I'm amazing at doing off the top of my head.
Sometimes repetition is just as important as discovering something new.

## March 9, 2016

### What did you learn yesterday?

Since I didn't write yesterday, I'll try to briefly cover yesterday and Monday.

On Monday, I paired with Michael, who showed me the basics of getting a Node environment set up. We
talked about how design works on the front end, with a focus on reusable components, rather than building
pages as a whole. It was cool to see, and I'll probably spend some time in the future learning more about
it just so I'll be a more versatile developer.

Yesterday I paired with Jordan, and we worked on a Keystone API. Everything feels so oddly similar but
different. The underlying principles are the same, but working with that made me appreciate Rails.

### What are you going to do today?

Today, I'll be pairing with Nick Cook in the afternoon. In the meantime, I'll continue to work on any
SmashingDocs bugs that come up, and I'll continue work on a web scraper that I started on Friday.

### What do you expect to learn?

I'm getting some experience with supporting software that others are using. Most everything I've built
thus far has either been for personal use, or an assignment that doesn't get used after it's done.

With my scraper, I've been improving requests, timing, file output, and I expect to learn some more
about refactoring and hopefully solidify the principle of single responsibility. I understand the principle
itself, but sometimes it can be hard to see the division of where one responsibility ends and where
another begins. The only thing that will make this better, however, is practice.

## March 7, 2016

### What did you learn yesterday?

I added the last SmashingDocs config yesterday, and it was pretty straight forward. It would have gone
faster had I not typed the folder name wrong into the config and thought things were broken. During
labs time, I started learning about how to write a web scraper. This is something I've wanted to learn
for a while, but for one reason or another, I just haven't. The code for them is rather simple, compared
to something like a standard Rails project. The hard part is getting to the data you need using the proper
requests, and parsing the data into a usable format with Nokogiri.

### What are you going to do today?

This morning, I'll be continuing work on the scraper I'm writing. The Nokogiri gem is good to have
familiarity with, so I'll use my time in the mornings for that this week. This afternoon, I'll be
pairing with Michael. Once again, I'm not sure what we'll be covering, but I'm sure I'll have plenty
to report tomorrow.

### What do you expect to learn?

From writing the scraper, I think I'll gain some experience with investigating how sites structure their
requests, and the ways they handle getting data on the page. Also, I should get some practice in building
a proper data structure to handle the data coming in without just generating a Rails model.

As far as pairing with Michael, I don't know at the moment, but I'm sure it'll be a lot.

## March 4, 2016

### What did you learn yesterday?

So, some things got rescheduled yesterday, and I ended up pairing with Annie for the afternoon.
We worked on implementing file upload with MongoDB. Everything relating to MongoDB was new to me,
so I got some basics about how a no SQL database works. I also realized how much I had relied on Rails
magic for file upload in the past. Everything is done in a much more manual way when dealing with an
API. I learned a bit about creating a tempfile and using that to get the file passed to the model.

### What are you going to do today?

While working with Annie yesterday, I noticed that her app folder name and wiki folder names didn't
match up. It dawned on me that this is probably a common thing and that I should address the behavior
for pushing to the wiki in SmashingDocs. I've decided to add a config for this, and will be working
on that this morning. Depending on how long that takes, I may or may not go back to writing automation
tools/scripts.

### What do you expect to learn?

Adding the new config shouldn't be too different from what I've done with the other configs. I've
been learning lots of little things about my editor/environment while building tools like my thor script
and the controller snippet I wrote yesterday. I expect that I'll continue to learn more of the same today.

## March 3, 2016

### What did you learn yesterday?

Yesterday I got an intro to Android development. I learned about the basic structure of
an Android app, like fragments and activities. I learned how events are handed off
between fragments and other apps. Tyler did a great job of covering a lot of material
in a rather short amount of time.

We worked in Android Studio, and he reminded me that I kind of miss working in a
full IDE. I may give RubyMine a shot at some point, just to see if I prefer it over
Atom, but I'm sure it'll come with a learning curve.

The hardest part of learning about new things is trying to find time to continue
learning about those things. I've been intrigued by mobile development for a while
now, but haven't really pursued anything with it. I feel like I have enough of a
foundation to build a very basic app, but now I just need to find the time to build one.

### What are you going to do today?

This afternoon, I'm pairing with William. Annie says that he has been working on
some interesting projects lately, so I'm looking forward to see what we'll be working
on today.

### What do you expect to learn?

I may mess around with RubyMine some today before I start pairing. SmashingDocs is
good to go, and I don't have anything else that I'm responsible for during the pairing
tour, so I'd like to utilize that time to learn some things.

## March 2, 2016

### What did you learn yesterday?

Yesterday I learned how your experience level as a dev influences the way you approach
software design. My current design approach is to find a place within the app that
seems appropriate to put the new behavior into, and start building it there. Since
starting up my career in programming, my approach has evolved from "make this thing
work" to "make this thing work and write it decently". After pairing with Brian yesterday,
I have seen the mindset of an experienced dev, and it's a very different approach.

As we worked together, we talked about what the feature needs to do today, where it
may be best to put different pieces of the behavior, what this feature might need to
be capable of, and how best to write this feature to be easily extendable in the
future without writing out a bunch of behavior now that may never be used.

I may not be able to put everything I learned into practice right away, but it
seems like another step on the way to becoming a better coder.

### What are you going to do today?

SmashingDocs seems like it is ready to be used, so hopefully that message can be
passed around the office today. I may work on DRYing up the test suite for it.

This afternoon, I'm pairing with Tyler, (Tyler McCraw, my coworker, not myself in
the 3rd person). I'm not sure what we'll be working on, but I know every day of pairing
will be unique.

Also, Brandon asked for some feedback on the apprenticeship lecture series, so I'll
write that up for him today.

### What do you expect to learn?

Like I said, I'm not certain what will be covered today in my pairing session, but
I'm sure I'll have a lot to write about tomorrow.

## March 1, 2016

### What did you learn yesterday?

Starting the new month with the new post instead of waiting 2 weeks. See, I'm learning here.
Yesterday I spent the second half of the day pairing with Derek, and about an hour meeting
with Lucas and Andy from Design.

From pairing with Derek, I got some experience with the workflow of a client project.
He did a great job of giving me some background on Jira, picking work from sprints/backlogs
and taking an issue through development and on to code review. A couple things stood out to
me yesterday. One was that the problems we were working on totally felt like issues I could solve,
so that gave me confidence that I'll be able to contribute to client work and be a productive
team member. The other thing I noticed was that Derek came to solutions on issues that came up
much faster than I would have. I think that's one of those skills that comes with experience.

I also got some insight into what the design team does beyond just making things look good.
There seems to be a lot of thought and work that goes into every design decision, and there is
a lot more involvement with the client than I first realized. Rather than being a segmented piece
of development, design seems to permeate all the steps from start to finish in our projects.

### What are you going to do today?

This morning, I'll be fixing some documentation on SmashingDocs. It's missing some instructions
regarding the new configs. This afternoon I'm paring with Brian, so I'm sure I'll learn a lot of
new things from him.

### What do you expect to learn?

It's interesting to see everyone's different workstyles. Everyone approaches things a
little differently, and I think this pairing tour will help me get a view of all the
different styles people have here.
