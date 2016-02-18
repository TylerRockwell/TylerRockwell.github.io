---
layout: post
title: The Ongoing Smashing Boxes Progress Post
description: "Where I'll write about all the wonderful things SB teaches me"
tags: [career, progress, smashing boxes, learning]
---

## February 18, 2016

### What did you learn yesterday?

I gained some insight into SmarfDoc, now renamed SmashingDocs, yesterday. Essentially,
the way it was initially written used a `Thread` that acted like an instance of the
`SmarfDoc` object. All calls were made on class methods that called instance methods.
I thought that maybe the class methods could be removed, and the test suite could reference
an instance variable instead. Unfortunately, I learned that persisting data from
the start to the end of a test suite is difficult, and neither minitest, nor RSpec
offer very good hooks to work with. The trouble with minitest is that there is a
`Unit.after_tests` hook, there is no `before_tests` hook to initialize an instance
of an object. RSpec, on the other hand, offers `config.before(:suite)` and
`config.after(:suite)` hooks, but variables declared within the suite scope are
not accessible by the individual tests. In RSpec, I *can* get away with using
a global variable, but just because I can doesn't mean I should.

### What are you going to do today?

I'm going to try to get the gem deployed as it is today. I rewrote the documentation,
and added an information hash so users can pass in multiple types of messages (at the
same time if they'd like). It can currently be added to the Gemfile with its
Github path specified, but it'd be better to just say `gem 'smashing_docs'`. Once that's
done, I'll be working on creating rake tasks for it to automate installation and
configuration of the gem.

### What do you expect to learn?

I know very little about building gems, so basically everything I do today will
be new to me. So for today, it looks like I'll learn to deploy a gem to rubygems,
and I'll learn to write rake tasks.

## February 17, 2016

### What did you learn yesterday?

I started doing a major refactor to SmarfDoc yesterday. I spent a lot of time
just going back and forth through the code, following program flow and trying
to understand everything that was happening. I wasn't sure if this was something
I would be able to work with until yesterday afternoon. I managed to remove a lot
of duplicated logic, reduce the complexity of parameters being passed around the
program, and rewrite other parts just for the sake of readability. I gained some
insight into working on other people's code and learned how important it is to
Google something you're unsure of. For some parts of the program I was able to learn
more about how they work (e.g. Building ERB templates with binding), and others I
discovered were just names that were left over from the gem's previous name
(Doc yo' self).

Aside from that, Annie and I paired yesterday, and she helped me refactor my "most popular"
sort on the bookstore to be done inside of a database query rather than in an array.
This array was causing problems with using Draper, and just kept causing issues
in the rest of the app. That's a great sign that code needs to change. So, if you're
interested to see how to sort on a calculated field directly from the database, this
is how it's done. My original code was in an earlier post, but here it is again.
`all.includes(:order_items).sort_by(&:times_sold).reverse!` This code is a scope
on the `Book` class. `times_sold` is also an instance method on book that sums
the `quantity` of book's `order_items`. The complication comes from the `quantity`
field. Sorting by `count(order_items)` would have been much easier. It took some
time, but we eventually got it to work. I'm not certain I'd have figured this out
without her, so a big thanks to Annie for taking the time to work on this with me.
The final code is as follows:
```
scope :most_popular, lambda {
    joins("LEFT OUTER JOIN order_items ON order_items.book_id = books.id")
      .select("books.*, coalesce(sum(order_items.quantity),0) AS total_quantity")
      .group("books.id")
      .order("total_quantity DESC")
  }
```
The `left outer join` makes sure to include books that have not been ordered in
the list. `sum(order_items.quantity)` seems self-evident, but `coalesce` must be
used to get books without sales to return 0. By default, Postgres returns `null`.
When using `order` on this field, the null cases show up at the top of the list,
which is exactly the opposite of what I needed. From there, just group on `books.id`
and order on `total_quantity`. Now I don't have an array floating around that needs
special treatment. This returns the proper ActiveRecord relation, and it does so
all in one query to the database. I'm certain I will run into this issue again in the
future, and it will be nice to have this code to refer back to.

### What are you going to do today?

Today, I'll make some final tweaks to the last code review on the bookstore. I'm
going to get some goals set for the SmarfDoc refactor (into the new and improved
Smashing Docs). It seems to be in a place where it is extendable now, so adding
functionality won't be quite so tedious and confusing.

### What do you expect to learn?

I'll likely gain some experience to planning out a project today. Everything thus
far in the apprenticeship has essentially been dictated through the apprenticeship
curriculum, but this project doesn't have predefined criteria in place already. I've
planned projects before (ArtTrack), and I think they were scoped well and went smoothly,
but more experience is always a good thing.

Also, Jordan mentioned ActiveSupport::Concerns yesterday in my pr, so I'll ask around
about them today and learn what I can about setting one up. About half the methods
on my `Book` class are *concerned* (see what I did there? It's okay to sigh...)
with the price of a book, so it'd be nice if I could move that logic into its own
place.

## February 16, 2016

### What did you learn yesterday?

I spent most of yesterday chasing production bugs. There were a bunch of issues
with API keys and email needed to be configured to work in production. I learned
that just because your rails app can see the keys (they work in rails c), there's
a chance they still may not work anyway. Everything worked once I moved from using
environment variables in my `secrets.yml` to just pasting the keys directly in.
It's in `.gitignore` and on the production server, which I don't push from, but
a part of me is still irked by putting keys directly in a file within the repo.
I'll likely look into better ways of managing keys in the future.

### What are you going to do today?

Near the end of the day yesterday, I started work on the discount feature of the
bookstore. It's up and working now, but it needs to be cleaned up some, so that's
what I'll work on this morning. After that, I'm not entirely sure what I'll be
working on. It may be SmarfDoc. I've been trying to unravel that during my free time.
It'd be nice to allocate more time to it.

### What do you expect to learn?

I'm still working out where to fit features like discounts in. I integrated it into
the `Book` model and the `create/update` actions of the `BooksController`. It works
there for now, but I think if the feature got any more advanced it may need to be
moved out into its own class. I think the more I write, the clearer these decisions
will become. Or at the very least I'll have a better understanding of the criteria
on which I should base that decision.

## February 15, 2016

### What did you learn yesterday?

Yesterday (Friday), I learned how to use Tape, which is an internal tool for deployment.
I got my bookstore deployed onto a Digital Ocean droplet, which of course, included
all the inevitable deployment bugs. Honestly, it's not all that bad. I need to get
email up and running from the deployed app, and everything else seems to be discrepancies
from using sqlite3 in development and postgres in production. (I should not have
been using sqlite3 in the first place).

I also redid the Gilded Rose kata, because repetition is key. I noticed, however
that the way I write methods, and my naming conventions have changed a lot over
the past few weeks. It hadn't really been obvious until I looked back at how I had
previously solved it.

For example, I wrote this method the first time around
```
def daily_adjustment(item)
  change = 0
  change += degrading_item?(item) ? -1 : 1 + backstage_passes_modifier(item)
  change *= conjured_item_modifier(item)
  change
end
```
If you stare at that long enough, you may be able to figure out what it's doing.
It works, and the tests pass. However, when I did the kata again this method turned
out like this
```
def daily_quality_adjustment(item)
  if better_with_age?(item) || time_sensitive?(item)
    improve_item(item)
  else
    degrade_item(item)
  end
end
```
I think that is much clearer at first glance, and while much of the underlying logic
is the same, it seems my thought process and naming conventions have changed drastically
over the past few weeks.

### What are you going to do today?

Today, I will be addressing the production bugs in the bookstore. I'm going to add
the discount feature soon as well, but I need more detail about what is expected
from that feature. I also don't want to try building new features on top of an
app that is not working correctly, so I'll start the day with bug fixes.

### What do you expect to learn?

I expect to learn some about postgres and configuring ActionMailer in production.
I know that pg won't allow you to use the LIKE operator on non-text fields. I may
just end up switching everything to ransack as there's no need to reinvent the
wheel here.

## February 12, 2016

### What did you learn yesterday?

Yesterday, I learned how to write a service layer. Essentially, a service is plain
Ruby class that houses a bunch of related behavior, typically between many objects,
that doesn't fit into the standard MVC architecture. In the case of my bookstore,
I needed one for the checkout process. Things like creating charges, emptying the
cart, and sending an invoice definitely don't belong in a view, they don't quite fit
into a controller (not to mention they make it bloated), and don't go along with
any one model. I do have some behavior defined in a model, such as `.empty` in the
`Cart` class, but the call to that method comes from the service. A service typically
has one exposed method and several private methods. The one public method is called
whenever the service needs to run, and everything happens within the private methods.
Clean code, ftw!

I also set up `stripe-ruby-mock` for testing the service yesterday. When I first
started putting the spec file together, I didn't really think I'd be able to test
all the behavior. However, I put everything together one small step at a time, and
now my service has fully tested behavior. Tests are time consuming, but they are
so wonderful when it comes time to refactor or add new behavior.

### What are you going to do today?

So, the bookstore feels pretty done. It's not the most beautiful project I've put
together, but with all the brilliant front-end, UI/UX, and design people here,
I'm sure nobody needs my input on how a site should look anyway. I know there are
new features being introduced to the bookstore, so I need to find out what those are
today and I'll work on getting them implemented. Annie says my code is clean enough
that it shouldn't be difficult to add, so here's hoping she's right.

### What do you expect to learn?

I'm fairly certain the new feature will be including discounts for purchases without
altering the original unit price of a book. I know that a deployment is coming soon
as well. So, at the very least, I will gain experience with these processes. It seems
that a big part of coding well (and in less time) is seeing similar problems arise
and knowing how best to overcome them. Throughout this app, and the apprenticeship
in general, the things I've seen before (like setting up REST actions for a new resource),
tend to go quickly and smoothly, while new problems are time consuming and require
a lot of thought and research. So, at this point I'm not exactly sure what I'll learn
today, but I know I'll at least gain experience.

## February 11, 2016

### What did you learn yesterday?

The bookstore is now feature complete. The most popular sort was easier than I
anticipated. All I did was put the relationship between `OrderItems` and `Books`
back in place (I had previously removed it, thinking it was not needed). To get
the times sold for each book, I just iterated through the books' `order_items`
and sum the quantity of each. To sort by most popular, looks something like this:
`all.includes(:order_items).sort_by(&:times_sold).reverse!`. Not nearly as bad
as I expected, and the `includes` keeps the database overhead low.

I got a brief intro to services yesterday as well. Annie is supposed to talk about
them more with me today.

### What are you going to do today?

Today I'm going to refactor some areas of the Bookstore and add some polish to it.
There are areas where currency isn't formatted properly, addresses are shown as
objects rather than the data they contain, etc... There is also some code that could
just be written better and relocated to make the app cleaner. So, most of my day
will likely involve addressing these things.

### What do you expect to learn?

I expect to learn about creating and implementing a service to handle behavior that
doesn't quite fit into a model, view, or controller. The most obvious example in my
app being the checkout process. The other things I need to do today are things that
I know how to do but haven't prioritized because they take time. Now that the app is
feature complete, I can take time to work on those things.

## February 10, 2016

### What did you learn yesterday?

So, I got to a lot of the things I listed yesterday. I didn't change statuses much,
but I added admin features, invoice emails on order completion, and paying with
saved credit cards. I spent the most time working with credit cards and Stripe again.
I learned how to save a customer token and retrieve a customer from Stripe with it.
I also got to work with my favorite language, Javascript, and every time I do that
I at least gain familiarity with it.

### What are you going to do today?

The primary goal for today is getting the most popular sort to work. Outside of
that, all I have left to do with the bookstore is allow admins to create more admins
and finish up some tests. Also, I believe orders paid for with credit cards may
not have a billing address set, so I'm going to look into that today as well.


### What do you expect to learn?

I've been thinking about how to set up the most popular sort order, and I think
I'll learn something today about writing efficient algorithms. Also, I expect to
learn about testing sort order in rspec.

## February 9, 2016

### What did you learn yesterday?

I learned about the methods ActiveRecord provides when you create an association.
I had used build when creating forms with nested attributes, but didn't realize how
versatile that functionality is. I've essentially been writing code for a while
that duplicates these provided methods. I've also gotten some more insight into
refactoring methods into smaller methods with a single responsibility. Doing so
sometimes reveals behavior that shouldn't even be in the class being refactored.
There are more subtleties to write about as well, as I learn a lot any time I pair
with Annie, but I could likely write half the day if I wrote everything down.

### What are you going to do today?

I have quite a bit to do today. I'm changing how order statuses are handled and
assigned. I'm going to add in a few small missing admin features, like a view
of all orders and the ability to create new admins. Beyond that, I need to finish
up some tests and add in the ability to sort by most popular and allow users
to pay with a saved credit card. I don't think I'll get to all of that today,
but I think it's good to take inventory of where I'm at.

### What do you expect to learn?

I expect to learn a bit about assigning statuses to orders, and about the larger problem in
general. Annie and I discussed how this tends to come up often and how it doesn't
seem to have one optimal solution yet. Outside of that, I'll likely learn the best
way to approach handling saved customer data from Stripe. I don't want to store
customer credit card information in my database, so I'll need to note that the
customer has a saved credit card and have a way to retrieve it.

## February 8, 2016

### What did you learn yesterday?

I've really got to start leaving myself notes or something on Fridays. I learned
that it's good to discuss things with the team when requirements don't seem clear.
If something isn't clear to me, then it likely isn't clear to others as well. I also
learned that while Stripe Checkout is a nice drop-in solution, its limitations are
quickly recognized when trying to build any custom functionality around it.

### What are you going to do today?

I'll be working on putting together a custom checkout form that integrates Stripe.
The checkout process is working at the moment, but not exactly the way I need it to.
Depending on how long that takes, I may also add in some miscellaneous features that
are still missing from the site like Admins creating more Admins, and the ability
to see a list of orders on the site.


### What do you expect to learn?

I expect to learn how to add Stripe fields to a form and handle responses from their
API. I'll likely have to add a check to make sure the credit card charge goes through
before submitting an order. I think this is another thing that will take some time
to set up initially, but once I know how, should be much faster in the future.


## February 5, 2016

### What did you learn yesterday?

I learned that entering data into a Stripe form with Selenium is more complicated
than it initially appears. The test needs to wait for the form to appear, which
it does not by default. Then, the fields must be selected and entered in a particular
way. The credit cart number, for example, must be broken into 4 inputs. Trying to
enter a string of `'4242424242424242'` will not work. Nicholas Rutherford has this
[awesome gist](https://gist.github.com/nruth/b2500074749e9f56e0b7) with the currently
working steps.

I also learned that while some things are more complicated than they first seem, but
it is also equally plausible that you're perceiving things to be more complicated
than they are. I spent a lot of time overthinking the checkout process of my bookstore,
but today I've realized that it may not need to be as difficult as I was making it
out to be.

### What are you going to do today?

I'm going to work on the checkout process of my bookstore today. I will be attempting
to use Stripe only for the payment part of the transaction and use my own forms
for all other data collection. I'm not entirely sure how I'm going to implement
the ability to remember/retrieve customer payment data, but for now I'm not going
to worry about it. It'll get worked out eventually.


### What do you expect to learn?

I'll get a refresher on nested forms. I've done them in the past a few times now,
but I still need to reference older work to build them. I'll likely learn a bit more
about managing customer payment information with Stripe. Also, I expect that once
this is done, I'll have a better understanding of how the checkout process should
work, and it should take significantly less time in the future.

## February 4, 2016

### What did you learn yesterday?

Yesterday I learned that if you have a controller for something, but no model,
that may be a good hint that you need that model. Case in point, I set up order
functionality on my bookstore that had cart-like functionality. It even had a
CartsController, but no cart model. It instead used Orders in various states to
keep track of whether items had been purchased.

This worked, but I had the Order class trying to do to much. Annie described it as
going to the (physical) bookstore, and instead of using a cart, just bringing
books to the cashier and leaving them there while you continue to shop. Does it
work? Yes. Is it awkward? Also yes. In that case, and the case of my app, it's
easier to just have a cart.

### What are you going to do today?

I built the cart model yesterday, and I restructured some of the underlying data
to work more sensibly together. I'm waiting on a code review now before moving
toward placing orders and charging customers. Since I went at things a little
backwards, order functionality is in place, I just need to set up payment processing
and handle moving items out of the cart and into a purchased order.


### What do you expect to learn?

I expect to learn about handling payments through Stripe and the order completion
process. As always, I'll likely pick up something new about Cucumber as well.

## February 3, 2016

### What did you learn yesterday?

I learned some new things about Cucumber and the Selenium driver yesterday. I set
up tests that could find an element in a particular row of the DOM. I also learned
how to test javascript popups with it. Annie helped me to set up Hound and Rubocop
on my project as well. It's helped to take away some of the uncertainty I had while
writing code in regards to style. I went through and linted my entire bookstore app
yesterday. Now I'll know before I submit my PR if some random file has an extra
blank line or is missing a space before a }.

### What are you going to do today?

Heh, this seems like the most difficult question to answer. Whatever I write here
is usually wrong. It really should say, "what do you think you're going to do today?".
I did finish up the order (I think order is more descriptive than cart for what
they are doing) models yesterday and implemented most of the integration
tests for now. Today, I'll set up the order controllers and get the models up
and doing something.


### What do you expect to learn?

Again, I'll likely gain some knowledge about setting up order/cart functionality.
I feel like if I mention Stripe here again, I'll never get to it, so I just won't.
There. I didn't say it.

## February 2, 2016

### What did you learn yesterday?

Yesterday, I learned how to set up email confirmation using Devise and Mailgun.
I had used Mailgun previously, so the setup for that was pretty straight forward.
Configuring the Devise end of things was easier than I expected. Once Devise is
set up, it's just a matter of setting `:confirmable` in the model and running a
migration. I learned to test this functionality as well. In order to use Factory
Girl, whenever an account is created, you must run `user.confirm` for that user
to be able to log in.

### What are you going to do today?

Today, I'm going to finish adding integration tests for the functionality that is
in place. I'll be finishing up the cart today and possibly implementing Stripe.


### What do you expect to learn?

I expect to gain some familiarity with building a cart. I have a general idea of
the structure that needs to be in place, but since I haven't built one before,
I'm bound to learn something about the details of putting one together. If I make
it to Stripe today, I'll learn about connecting my app to their API.

## February 1, 2016

### What did you learn yesterday?

So, apparently I missed a day (of blogging, not work). So to recap what I did over
the past few days. [I learned some things from the Gilded Rose kata]({ % post_url 2016-02-01-lessons-learned-gilded-rose % }).
I got some practice in Gem modification and working with legacy code. Finally, I
learned that if there's a good gem for a common task, you should use it. Don't just
throw every gem you come across into your project, of course, but they can save
you a ton of time and effort.

### What are you going to do today?

I'm going to continue working on the Rails Bookstore. Books, users, admins, sort,
search, and pagination are all in place. I'll work on creating new users while logged
in with Devise so admins can create more admins. Also, I need to get the email
confirmation functionality up and running. Beyond that, I need to move towards
implementing a cart and payment processing.

### What do you expect to learn?

I expect to learn some more things about Devise. It's gotten much easier to setup
now that I've used it some. I can have an authentication system up and running in
a couple minutes now instead of half an hour (or all day, like the first time with
Devise). Most of my time will likely be spent on that and finishing the bowling
scorer kata today.
