---
layout: post
title:  "ES6 Status - Promises"
date:   2018-04-12
categories: javascript
---

### promises

Promises are often used when fetching data from APIs, AJAX and such. 

`.fetch()` is similar to `$.ajax()` and `$.getJSON`, however it is not loaded from some type of external library. Instead, is built-in/available in-browser and returns promises. 

*What is a promise?* Like it sounds, an IOU of something that will happen at some point from now till some point in the future, most likely, not immediate.

*Why would we need promises?* Based on the fact that JavaScript is all about being asynchronous, some times things get ran before other things needed are available. Promises are a good way to set up something to run, finish, and then moving on to the next thing.

Example:
```
console.log('Fetching...'); 

const posts = fetch('http://whateverwebsitehere.com/whatever-json/posts');

console.log('Done!');
console.log(posts);

```
^above will result in an console.log output of:
```
Fetching...
Done!
Promise { <state>: "pending" }

```

It goes to fetch whatever data, but doesn't get through it before 'done' is logged. It queues the request, it lets you know in a way that it is working on it and when the info is snagged it will return, hence `Promise { <state>: "pending" }` up there^.

*What can be done?* Using example above:

```
const postsPromise = fetch('http://whateverwebsitehere.com/whatever-json/posts');

postsPromise
	.then(data => data.json())
	.then(data => { console.log(data) })
	.catch(err=> { console.error(err) })

```

`.then()` is similar to `on-click`, meaning it will only run when it clicks or in this case only run when the data comes back.