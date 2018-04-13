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

### building promises

As somewhat mentioned above, promises are pretty much used when you want JS still running while waiting for something else to be dealt with upon completion. This seems pretty handy when waiting on API data.

Below is a simulation of a Promise contructor waiting to resolve. The idea is the setTimeout acts as time waiting on certain data to come through, once that happens we are notified of its resolve.
```
 const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('This promise was resolved');
  }, 2000); 
 });

 p
  .then(data => {
    console.log(data);
  })

```

In similar fashion, below shows promise rejected for whatever reason and having the error caught w/ information regarding error. However, using the `Error()` within `reject()` is what will be caught, directing us to where the Error took place. Without this, error would get caught, but the line shown would be where the catch err was placed and not actual reject/error line.
```
 const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject(Error('This promise was rejected'));
  }, 2000); 
 });

 p
  .then(data => {
    console.log(data);
  })
  .catch(err => {
    console.error(err);
  })

```

### chaining promises, flow control

Example below mimics snagging info from "database" using Wes's example of posts & authors. Specifically, a post of a certain ID.
```
  const posts = [
    { title: 'I love JavaScript', author: 'Wes Bos', id: 1 },
    { title: 'CSS!', author: 'Chris Coyier', id: 2 },
    { title: 'Dev tools tricks', author: 'Addy Osmani', id: 3 },
  ];

  const authors = [
    { name: 'Wes Bos', twitter: '@wesbos', bio: 'Canadian Developer' },
    { name: 'Chris Coyier', twitter: '@chriscoyier', bio: 'CSS Tricks and CodePen' },
    { name: 'Addy Osmani', twitter: '@addyosmani', bio: 'Googler' },
  ];

function getPostById(id) {
 // promise created
 return new Promise((resolve, reject) => {

  // setTimeout to simulate having to wait for some data to come through
  setTimeout(() => {
    // finds post, self-explanatory
    const post = posts.find(post => post.id === id);
    if(post) {
      resolve(post);
    } else {
      reject(Error('No Post Found.'));
    }
  }, 2000);
 });
}

getPostById(2) // once post id snagged
  .then(post => { console.log(post) }); // then, output result

```

When we get back our specified post, posts.author contains name only, to replace that with info from authors object of particular author with more information...

we create another function `snagAuthorInfo(post)` where the post we snagged by ID will get checked for `post.author` matching `authors.name` in authors array of objects. If one is found, the author obj will then replace the `post.author` string. If none found, an error will return stating no author was found.
```
  const posts = [
    { title: 'I love JavaScript', author: 'Wes Bos', id: 1 },
    { title: 'CSS!', author: 'Chris Coyier', id: 2 },
    { title: 'Dev tools tricks', author: 'Addy Osmani', id: 3 },
  ];

  const authors = [
    { name: 'Wes Bos', twitter: '@wesbos', bio: 'Canadian Developer' },
    { name: 'Chris Coyier', twitter: '@chriscoyier', bio: 'CSS Tricks and CodePen' },
    { name: 'Addy Osmani', twitter: '@addyosmani', bio: 'Googler' },
  ];

function getPostById(id) {
 // promise
 return new Promise((resolve, reject) => {

  // setTimeout to simulate having to wait for some data to come through
  setTimeout(() => {
    // finds post, self-explanatory
    const post = posts.find(post => post.id === id);
    if(post) {
      resolve(post);
    } else {
      reject(Error('No Post Found.'));
    }
  }, 2000);
 });
}

function snagAuthorInfo(post) {
  // new promise
  return new Promise((resolve, reject) => {

    // find author
    const authorDeets = authors.find(author => author.name === post.author);
    // if author, replace org author string with author object
    if(authorDeets) {
      post.author = authorDeets;
      resolve(post);
    } else {
      reject(Error('No Author Info Found'));
    }
  })
}

getPostById(3)
  .then(post => { 
    // console.log(post) 
    return snagAuthorInfo(post) // returning a promise allows to chain another then()
  })
  .then(post => {
    console.log(post);
  })
  .catch(err => {
    console.error(err);
  })

```

