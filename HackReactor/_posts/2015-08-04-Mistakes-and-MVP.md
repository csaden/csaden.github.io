---
layout: post
title:  Day 32&#58; Mistakes and MVP
date:   2015-08-04 20:29:22
categories: HackReactor
comments: true
---


### What did you learn today?

I learned how to put together a full stack, including Sequelize/mySQL, Angular, Node.js, and Express.js, to build a minimum viable product. I was fairly confident that what I had scoped would be possible over the two days, but I began to doubt my ability to finish the project soon after lunch. I struggled for the last few hours to get my router on the server to work correctly. I knew I had all the client side code and database retrieval set up properly. After tracing my steps over and over again through the code, I realized that I forgot to create an express router to use '/api/response' in my middleware and to pass that router into the appropriate routes file. It was a painful lesson, and I wish my debugging skills would have gotten to that point sooner.

In the end, my [Writelet](https://github.com/csaden/2015-06-mvp) application came together 5 minutes after the MVP presentations started. I quickly created a prompt and logged some responses so the database would be populated for the demo. The demo took only one minute of time, and before I knew it I was back in my chair listening to the other demos: a music visualizer, a simplified Yelp, a Boggle-like word game, a memory game for remembering peoples name, and many many others.

In the end, I was super impressed with all of the ideas and code that my cohort created. I'm also glad that I had the chance to go from scratch, literally zero lines of code, to a bare bones client and server in under 48 hours.

### Did you learn anything new about yourself?

I need to retrace code more logically when it comes to debugging. I need to keep asking what assumptions am I making about how my code is running. For the MVP sprint, I made small mistakes when it came to hooking up all the pieces: adding script tags, adding module names, injecting dependencies, and connecting routes with their route handlers. Some of these silly mistakes cost me an hour of debugging, and I know I can do better in the future.

### Anything you want to do differently tomorrow?

I want to solve arraySum and asyncMap toy problems. I've struggled to solve these problems, and I need to come up with better diagrams to crystallize my thinking and my approach.
