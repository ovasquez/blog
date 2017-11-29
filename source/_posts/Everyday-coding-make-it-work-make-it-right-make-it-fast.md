---
title: 'Everyday coding: make it work, make it right, make it fast!'
date: 2017-11-28 17:19:41
tags:
- coding
---

I have heard this phrase in several occasions, but always thought it was just a catch phrase to motivate people to code more and stay working late. With all the buzz words you hear at work, why would this one be any different?

I decided to explain it to my ten-years-ago self that didn't take the time to read between the lines.

## A bit of context

As a software developer who has worked in different companies (small, medium and large sized), I've been exposed to quite a few development methodologies, each one of them clamming to be the holy grail of software development. This has given me a good perspective on the pros and cons, and allowed me to understand some of the core skills and values that are common among them.

You might be thinking, what does the catch phrase have to do with the development methodologies? These are simple cues for successful code writing, which is vital in any methodology you choose.

Let's take a look at the phrase again, but this time in more detail:

## Make it work
You have an idea of what's the goal but you still haven't connected all the dots, so, how do you begin?

I've tried TDD before, but this never worked well for me when dealing with a high level of uncertainty, so I rather take some time to explore options, understand inputs and outputs, while at the same time trying to find a way to make it by growing the codebase.

### TLDR
Start exploring the solution without expecting to solve all problems in the beginning.

## Make it right
Your code works. Now it's time to make it look good.

Think about clean code principles and look for parts of the code that are due for a refactoring.

- Did a file or a function get too big?
- What about some common functionality that could be unified?
- Any patterns you might have missed, or anti-patterns that made their way through during a long night of coding?
- Do you have repeatable tests to make sure your code keeps working after some tweaks?

This is the time to make it right.

### TLDR
Your code is working, clean it up, refactor it if necessary (patterns, low coupling), and write tests for the core functionality.

## Make it fast
The show is ready to start and you're about to publish your code, but performance could be a showstopper.

The code might not be in a critical section, but it's always important to keep in mind how it's going to be executed.

- Is this a simple UI tweak or do we have to execute thousands of requests per second?
- How about the memory consumption? Could we make it more efficient?
- Are we using the least amount of necessary CPU cycles?

This is usually best answered with performance testing, but even without it (or just with some simple tests), thinking about the performance when you have the complete picture of the code allows you to identify issues that could have been missed when delving deep into writing each line, look at this as is the *icing on the cake* before publishing.

### TLDR
Review the code for performance improvements (CPU, Memory, etc.) that you might have missed during the process.

## Final words
Regardless of the process, requirements, or level of abstraction that I have to work with, these steps allow me to have a common way to tackle most of the *everyday coding* tasks. I hope this was enough for my 10-years-ago self to get started in the good coding life 😎.