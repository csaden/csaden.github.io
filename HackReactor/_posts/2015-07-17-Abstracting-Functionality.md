---
layout: post
title:  Day 17&#58; Abstracting Functionality
date:   2015-7-17 23:06:31
categories: hackreactor
comments: true
---

### What did you learn today?

The day started with a toy problem, which left my head spinning. I worked on coding a solution to check if two objects were deeply equal (that is they have the same keys and values or structure). I tried to make as little assumptions as possible and thought about a recursive function that would check nested values in the object. This approach reminded me of coding a recursive parseJSON function in the pre-course work. Eventually, I abandoned that method and made use of stringify, which nearly worked with the exception of when object keys are in different orders.

That's probably way to much detail for today, but I wanted to write about it since my mind fixated on the problem throughout most of the day. The problem also doesn't take into account for checking for NaN or nested arrays and objects in the values. Perhaps, I made the problem more complicated than it was intended to be.

At any rate, the rest of the day went well. We tackled CoffeeScript syntax in the morning lecture, and then we learned a bit more about event listening and decoupling functions. The abstraction of event listening is powerful, and it's a wonderful feature of Backbone.js. For the new sprint, we started coding up a BlackJack application, and my pair and I talked through much of the code before writing our on lines. That was another exercise of great patient and reasoning. It paid off as we added a few lines of code to the app to achieve the desired functionality. We thought our code was slick. Tomorrow, we'll tackle some event listening for a "blackjack" and move on to extra credit.

### Did you learn anything new about yourself?

I read a lot! I skimmed close to 100 articles today, and I cleared out my work email once I got access to it again. An near-zero inbox made me happy.

I think I'm getting better about reasoning abstractly. My pair and I made good decisions about writing simple functions that could be reused throughout the application. We also thought about specific functionality that only applied to a dealer's hand and where that logic should live.

It takes a lot of effort to write readable and reusable code.

### Anything you want to do differently tomorrow?

I want to finish re-factoring the n-queens problem and create a plan for building up my front-end design and CSS skills.

