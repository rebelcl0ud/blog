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
however, inputting `dog.next()` will "return" or `yield` first object with value of `scrappy` along with `done: ` status. The status will show as false until it finishes running function. In this case, it will show `done: false` until AFTER sam output, then showing `done: true`

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

```
const inventors = [
  { first: 'Albert', last: 'Einstein', year: 1879 },
  { first: 'Isaac', last: 'Newton', year: 1643 },
  { first: 'Galileo', last: 'Galilei', year: 1564 },
  { first: 'Marie', last: 'Curie', year: 1867 },
  { first: 'Johannes', last: 'Kepler', year: 1571 },
  { first: 'Nicolaus', last: 'Copernicus', year: 1473 },
  { first: 'Max', last: 'Planck', year: 1858 },
];

function* loop(arr) {
  for (const item of arr) {
    yield item;
  }
}

const inventorGen = loop(inventors);

```
[^inventors ex used by wes bos]

multiple use of `yield` unnecessary (1st ex), using one like above will "return"/ yield each inventor.

input of `inventorGen` in console will output `Generator {  }` with dropdown of prototype methods built in such as `next()`.

`inventorGen.next()` outputs first object from above example, for quick display of info use `inventorGen.next().value`- will display `Object { first: "Isaac", last: "Newton", year: 1643 }` instead of `Object { value: {…}, done: false }`.
