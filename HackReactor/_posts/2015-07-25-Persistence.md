---
layout: post
title:  Day 23&#58; Persistence
date:   2015-07-25 00:35:03
categories: HackReactor
comments: true
---


### What did you learn today?

Today, we started a new sprint on databases. I am familiar with databases since I've queried Udacity's database using MongoDB, which is a no-sql (or schema-less) database. An example of a document for a no-sql database is included below. At Udacity I investigated common incorrect responses to computer graded questions. I tried to uncover instructional design flaws and student misconceptions from that that data and then improve the curriculum or the question. The data I looked at comes in the form of a document which you can think of like any Javascript object or Python dictionary with key value pairs. The keys are called fields in MongoDB and the fields can be nested. The schema-less or unprescribed structure allows for the storage of unstructured data. Here's an example of one such document.


{% highlight javascript linenos %}
{
  movie: 'The Matrix',
  lead_actors: ["Keanu Reeves", "Laurence Fishborn", "Carrie-Anne Moss"]
  ratings: {
    metacritic: 73,
    imdb: 8.7,
    rotten_tomatoes: 87,
    amazon: 4.5,
  }
  director: "Wachowski Brothers"
  awards: {
    academy_awards: {
      won: ["Best Film Editing", "Best Sound", "Best Sound Effects Editing", "Best Visual Effects"],
      nominated: []
    }
  }
  mpaa_rating: "R",
  duration: 115
}
{% endhighlight %}


The first hour or so of our time, however, was focused on learning SQL (structure query language) which makes use of relational tables. You can learn more about relational databases and mysql [here](http://www.sitepoint.com/getting-started-mysql/). We needed to hook up our chatterbox server to a "chat" database so that message and user data would persist for our application.

In a previous sprint, we built a chatterbox server that made use of temporary storage that reset each time the server started. This time around we were given server code, which used express.js. My pair and I stumbled our way through understanding the code we were given. It took a solid two hours or more to eventually figure out how the server made use of controllers and models to handle requests and responses for the client. We talked and discussed what we thought was happening, and then eventually code started to click as we were able to describe the desire functionality of the code we needed to write.

We originally over complicated our mental model of what to do. As we talked through small examples of what the client and server were supposed to do at each step, the code became more clear. I'm excited to learn more about express.js and what the code is abstracting away for us. My pair and I coded up most of the solution, and we need to figure out what's preventing our post request from being sent to our server (we only receive an options request).


### Did you learn anything new about yourself?

I am not afraid to articulate when I don't understand a topic or problem fully. I treat those moments with humor, laugh at myself, and then seek more understanding after I'm sure any feelings of frustrations have passed.

### Anything you want to do differently tomorrow?

I want to pseudocode with my pair before we actually write code tomorrow. I should also do that with my toy problem. I don't pseudocode my entire approach to a problem before coding, and I think my code would be better if I invested more time in clear and simple language first.

I found some awesome web resources from Team Treehouse on CSS and a playlist of their Team Treehouse Show. Nick Petit and his team have created 150 videos over 3 years. Impressive! I'd like to start go over some of these resources. If I tackle one video and resource a day, I should be able to get through it all in under 6 months. Granted, I hope some of the earlier content is out of date or no longer relevant so I can skip it. :)

I also want to consider writing and teaching software engineering, coding languages, and algorithmic thinking. Learning this stuff should not be so difficult that learning becomes discouraging, which it has at times. I think it might be due to a lack of clear explanations and examples. There's also this expectation, at least at HackReactor, that you must figure out problems. Learning is predominantly done through exploration, reading documentation, coding projects, and talking with peers. I wonder what other techniques could be used to aid in learning software engineering and all that I've learned at HackReactor.

Last thing, I want to start reading a book called ["Getting More: How You Can Negotiate to Succeed in Work and Life."](http://www.gettingmore.com) A friend of mine mentioned it to me over a year ago, and I could use some more advice and practice in negotiations.

