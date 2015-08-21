---
layout: post
title:  Day 26&#58; Hashing Passwords and Resolving Promises
date:   2015-07-28 23:33:25
categories: HackReactor
comments: true
---


### What did you learn today?

The sprint on shortly-express continued today. We hooked up an authorization middleware in the application to check the user's session before logging in. We had the entire application working at one point, and then we went down a rabbit hole trying to create a sessions table in the database (not knowing that express-session handles nearly everything for us). We also learned more about [Bookshelf](http://bookshelfjs.org/), which is an ORM (Object-Relational Mapping) for Node.js. Basically, Bookshelf makes it easier to turn data in code to data in a database; it's also simple to perform create, read, update, delete (CRUD) operations on the database. In the afternoon, my pair and I watched the solution video and discovered some smart refactoring techniques.

My biggest takeaway from the day dealt with separation of concerns. In our implementation of the application, my pair and I used code in the post routes for signup and login to encrypt and to compare, respectively, the user's password using [bcrypt](https://www.npmjs.com/package/bcrypt), an npm module. The solution showed a more advanced implementation, which stored the functionality of storing and comparing passwords on the user model. This made more sense because the user model may change and because passwords are specific to users rather than the route.

Here's that code. After the code, I'll try to explain what the code is doing.

{% highlight javascript linenos %}
var db = require('../config');
var bcrypt = require('bcrypt-nodejs');
var Promise = require('bluebird');

var User = db.Model.extend({
  tableName: 'users',
  hasTimestamps: true,
  initialize: function() {
    this.on('creating', this.hashPassword);
  },
  comparePasswords: function(attemptedPassword, callback) {
    bcrypt.compare(attemptedPassword, this.get('password'), null, function(err, isMatch) {
      callback(err, isMatch);
    });
  },
  hashPassword: function() {
    var cipher = Promise.promisify(bcrypt.hash);
    // return a promise - bookshelf will wait for the promise
    // to resolve before completing the create action
    return cipher(this.get('password'), null, null)
     .bind(this)
     .then(function(hash) {
       this.set('password', hash);
     });
  }
});

module.exports = User;
{% endhighlight %}

To re-factor the code that we originally wrote, I made three changes to the code. First, I created a `comparePassword` function. The function takes in the attemptedPassword from the login post request and a callback function. The attemptedPassword is passed into bcrypt's compare function as well as the user's stored password using a getter. The compare function in bcrypt returns either an error or a boolean for a match. To finish up the `comparePassword` function, I call the callback passing in the variables for the error and the boolean.

**Note this next paragraph is probably confusing. Consider it a work in progress.**

The second change was more difficult. I created a `hashPassword` function which returned a [Promise](http://www.sitepoint.com/overview-javascript-promises/). By promisifying bcrypt's hash function (yes, you can promisify a function thanks to [bluebird](https://www.npmjs.com/package/bluebird)), one can create a promise using a function and later run a callback when the function succeeds or handle an error when the function fails. The hash function takes in the original password on signup, hashes the password using a salt, and returns that hash which can be stored. It's the hash that I'm was after since the encrypted password or hash was meant to be stored in Bookshelf's users table (part of the database). Because the password is attached the model of the user's data, I needed to bind `this` to the call of the promisified version of bcrypt's hash function. The binding of `this` allowed me to use a getter to `this.get('password')` from the user's model on creation. I could then take the hash (the encrypted password from the promisified function call) and resolve the promise by using `.then(function(hash) {})`. Notice that I passed in the hash into the resolve of the promise. This allows me to now set the password on that user's model since I want to store the hashed password rather than the originally entered password on signup.

So why use the promise to begin with? Well, Bookshelf will wait to finish creating the user until the promise is resolved. This means that instead of storing the original password on the user model Bookshelf will wait until the promise resolves before completing the create action for the user. To make Bookshelf wait, I made one final change. I created an event listener.

{% highlight javascript linenos %}
initialize: function() {
  this.on('creating', this.hashPassword);
}
{% endhighlight %}

The initialize function on the user model listens for a "creating" event. When a new user is created in the Users collection, the "creating" event is fired as is the `hashPassword` function which lives on the user model. Bookshelf waits for the original password to be hashed, and then the Promise resolves by setting the hashed password. The user is saved into the database with the username and hashed password. Success!

Here's all of that User model code if you're interested.

### Did you learn anything new about yourself?

I like figuring out how libraries, frameworks, and modules work. It's pretty frustrating at first since I don't know much about the syntax or functionality, but after trying many approaches, looking at examples, and relying on my intuition, I eventually come to understand.

I learn just as much if not more by explaining re-factored code in writing than I do refactoring code in code editors.

### Anything you want to do differently tomorrow?

I didn't bring my lunch, which was a bit of a bummer. My pair and I had lunch at an awesome Vietnamese restaurant instead. I did manage to buy groceries in our afternoon break, and I'm hoping to make a summer corn soup.

