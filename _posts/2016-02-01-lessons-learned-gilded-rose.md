---
layout: post
title: Lessons learned from the Gilded Rose kata.
description: "Sometimes lessons come from nuances"
tags: [career, progress, smashing boxes, learning]
---

I learned something from the [Gilded Rose kata](https://github.com/jimweirich/gilded_rose_kata).
It turns out it was significantly easier and less time consuming to just drop a couple more if
statements into the already giant mess of if statements. With this approach I was
done in under two minutes with all tests passing, whereas before it took me over
an hour to properly refactor everything (compounded by not being able to touch
the item class).

At first, I thought to myself, "Wow, this kata sends entirely the wrong message."
It seemed to illustrate that making the 'wrong' decisions saves a huge amount of
time and effort. As I thought about it more, though, I realized that's exactly what
working on real code is like. It can be very tempting to make 'wrong' changes that
work because they're easier at the time. This is the way that code decays and
eventually becomes unmaintainable. Developers make instant gratification choices
with their code to get one piece working without thinking about the future.

If you're working on a project that will never be changed again, and does not need
maintenance (such as this kata), then the easy approach may be okay. If, however,
this project will need new features and need to be updated and maintained, it is
better to take the proper approach. What may take you an extra hour today could
potentially save days or weeks worth of work in the future.

This is the thought that developers need to keep in mind while working on their code.
Best practices are considered as such because they are what makes code readable
and easy to work with. However it's important to find the balance between refactoring
and implementing new features. If you endlessly refactor and try to get the code
perfect, you'll never be able to add new features. On the other hand, if you just
hack in new code and never think about how it should fit into the larger application,
you'll soon end up with an unmanageable mess of code where every small change breaks
several other pieces. So, like many other aspects of our lives, this principle
relies on finding balance.

This just goes to show that although you can learn a lot by trying out new tech,
using new gems, or tackling problems you've never seen before, there are also
subtle but profound lessons to be learned from things that you already know how
to do.
