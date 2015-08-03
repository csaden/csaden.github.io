---
layout: post
title:  Day 28&#58; Mongo and Mongoose
date:   2015-07-30 22:05:05
categories: HackReactor
comments: true
---

### What did you learn today?

Deployment sucks. Ok, it's not bad, but those were the words we first heard in lecture when starting the Shortly-Deploy sprint. We needed to deploy our app using Microsoft Azure, and I couldn't not help but think that deployment would be painful. As it turns out, most of the time I was running a bunch of commands in the terminal to set up a server in the cloud that would run my code as clients fired off HTTP get and post requests. I could see somewhat into how that black box was running by looking at the log tail of Azure when running the website. Unfortunately after the sprint, I feel like I have many holes in what industry staging and production looks like in practice.

In terms of more in-depth learnings, I learned about MongoDB and Mongoose, a Javascript ORM for MongoDB. Truth be told, I already had a solid understanding of MongoDB from working at Udacity and from taking [MongoDB for Developers](https://university.mongodb.com/courses/M101P/about), one of MongoDB's courses. Mongoose, on the other hand, was entirely new. It was easy enough to learn, and while it's syntax differs slightly from Bookshelf, the concepts underlying Mongoose match perfectly with those of Bookshelf. I'm spending the rest of the night refactoring the Mongoose implementation to be sure that I have the nuts and bolts committed to memory.

### Did you learn anything new about yourself?

I like to persist in the face of challenges. I've had some bugs in toy problems recently and I kept trying different approaches last night until I finally solved them.

I also confronted a challenging toy problem called ArraySum during one of my mock interviews with a senior. I needed to find the largest contiguous sum in an array. My initial approach missed potential maximum sums, and I needed my algorithm to run in linear time O(n). I still need to solve that problem so I'm going to add it to my morning tasks tomorrow.

"If there is no struggle, there is no progress." -[Federick Douglass](https://en.wikipedia.org/wiki/Frederick_Douglass)

### Anything you want to do differently tomorrow?

I want to try our last structured sprint at HackReactor solo! I'm pretty excited to program alone and talk to others as needed. Our next challenge is to build our client-side shortly application in Angular instead of Backbone. Ready, set, (ng)-o!