---
layout: post
title:  Day 15&#58; The Source of Truth
date:   2015-7-15 21:32:07
categories: HackReactor
comments: true
---

### What did you learn today?

I learned about MVC* architecture today and separation of concerns. In general, programs and smaller functions should be built in small parts. Functions should not necessarily depend on other functions. Instead, functions should have some input and produce a desired output. In Javascript and MVC frameworks, there's a lot of event driven behavior in which Views (V) take user input to trigger events. In Backbone, these events can be listened by Models (M) or Collections (C) to make changes to the underlying data (the source of truth), which in turn fire other events that the Views (V) can listen to in order to re-render themselves with the updated data changes. If this sounds confusing, it certainly is (at least at first). I'm making more sense of this each day.

At the start, I mentioned MVC*. The asterisk is for the C since some frameworks make use of Controllers and lack Collections. The main features of an MVC* application are routing, data binding, templates/views, models, and data access.

### Did you learn anything new about yourself?

I appreciate MVC* frameworks and the people who designed them. Before diving into the sprint today, my pair and I talked about the architecture of the application we were going to build and drew a diagram showing the relationships of the Models, Views, and Collections. This really helped cement our understanding of the application before starting. It took about a half hour or so to work through that together, but it was well worth our time. I learned that I do a bit better when I slow down and try to understand what code is doing before bringing my eager fingers to the keyboard to code.

### Anything you want to do differently tomorrow?

I want to continue planning and understanding existing code before tackling sprint projects. I stayed behind to make some specs pass and that time was well spent.

I also want to revisit previous toy problems to refactor code and write recursive functions without subroutines.