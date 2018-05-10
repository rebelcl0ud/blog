---
layout: post
title: ES6 Status - Generators
date: 2018-05-10
categories: javascript
---

generator functions offer multiple type returns using yield.

```
function* listDogs() {
  yield 'scrappy';
  yield 'enigma';
  yield 'sam';
}

const dogs = listDogs();

```
when inputting dog in console, output will give generator status info
however, inputting `dog.next()` will "return" or `yield` first object with value of `scrappy` along with `done: ` status. The status will show as false until it finishes running function. In this case, it will show `done: false` until after sam output.

the above example is hardcoded, but dynamically generated variables is possible, example below.
```
function* listDogs() {
  let i = 0;
  yield i;
  i++;
  yield i;
  i++;
  yield i;
}

const dogs = listDogs();

```
gist: generator functions will keep its variables until it is finished, and able to yield multiple values from it.


