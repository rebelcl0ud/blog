---
layout: post
title: ES6 Status - Async + Await Flow Control
date: 2018-05-16
categories: javascript
---

asyncronous vs. syncronous: syncronous is when one thing finishes before another while asyncronous can have a task start, then immediately move on whether that initial task finished or not.

async + await just pauses for certain info without blocking like an alert would do.

note: async + await is built on top of promises, it is not something seperate.

```
function breath(amount) {
  return new Promise((resolve, reject) => {
    if (amount < 500) {
      reject('too small of a value');
    }
    setTimeout(() => resolve(`${amount} ms done`), amount);
  })
 }

 async function go() {
  console.log('start...');
  await breath(1000);
  console.log('end')
 }

 go();

```
In console you will see output of 'start...' followed by 'end' after what seems to be a brief pause, which is the setTimeout of 1sec.

Note 1: `await` cannot be used top-level, you'd get an error in console, such as `SyntaxError: await is only valid in async functions and async generators`

Note 2: No callback nightmare, no chaining of `.then()`s, no scoping introduced (all one level).

```
function breath(amount) {
  return new Promise((resolve, reject) => {
    if (amount < 500) {
      reject('too small of a value');
    }
    setTimeout(() => resolve(`${amount} ms done`), amount);
  })
 }

 async function go() {
  console.log('start...');
  const res = await breath(1000);
  console.log(res);
  const res2 = await breath(5000);
  console.log(res2);
  const res3 = await breath(500);
  console.log(res3);
  console.log('end')
 }

 go();

```
capture value function returns^ displaying amount it took to be done, below is example console output of values resolved from promise function^

```
start...
1000 ms done
5000 ms done
500 ms done
end

```
if `await` was to be removed it would return a promise, but having `await` in front of the promise breath will return promise and put out a sort of notice to hold on for a few seconds to wait for (in this case) breath function to resolve or reject.



