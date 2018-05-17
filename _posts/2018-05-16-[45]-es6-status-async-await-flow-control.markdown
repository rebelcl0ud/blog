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

### error handling

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
  try {
    console.log('start...');
    const res = await breath(1000);
    console.log(res);
    const res2 = await breath(5000);
    console.log(res2);
    const res3 = await breath(300);
    console.log(res3);
    console.log('end');
  } catch(err) {
    console.error(Error(`oh snap: ${err}`));
  }
}

go();

```
^which will run as before, but w/ an amount to changed to < 500, we `catch` the error.

high order function route: *what is a high order function?* a function that takes in a function as an argument and returns a new function
```
function breath(amount) {
  return new Promise((resolve, reject) => {
    if (amount < 500) {
      reject('too small of a value');
    }
    setTimeout(() => resolve(`${amount} ms done`), amount);
  })
 }

// fn is any function, such as something like -> .map(function(){ })
function catchErrors(fn) {
  return function() {
    return fn().catch((err) => { 
      console.error(Error(`whoooa -> ${err}`))
    });
  }
}

async function go() {
  console.log('start...');
  const res = await breath(1000);
  console.log(res);
  const res2 = await breath(5000);
  console.log(res2);
  const res3 = await breath(300);
  console.log(res3);
  console.log('end');
}

// go(); instead of this
const wrappedFn = catchErrors(go);

wrappedFn();

```
a high order function would stream lines catching multiple errors by wrapping into another function that would act as a catch all

breaking it down:
a function `catchErrors` that returns another function that then returns a function that runs with a catch tacked on the end.

running `wrappedFn();` is not running `go`, instead we've wrapped `go` in `catchErrors` that outputs brand new function `wrappedFn`

*what about if `go` took an argument?*
```
function breath(amount) {
    return new Promise((resolve, reject) => {
      if (amount < 500) {
        reject('too small of a value');
      }
      setTimeout(() => resolve(`${amount} ms done`), amount);
    })
   }

   // fn is any function, such as something like -> .map(function(){ })
   function catchErrors(fn) {
    return function() {
      return fn().catch((err) => { 
        console.error(Error(`whoooa -> ${err}`))
      });
    }
   }

   async function go(name) {
      console.log(`${name}, starting...`);
      const res = await breath(1000);
      console.log(res);
      const res2 = await breath(5000);
      console.log(res2);
      const res3 = await breath(300);
      console.log(res3);
      console.log('end');
   }

   // go(); instead of this
   const wrappedFn = catchErrors(go);

   wrappedFn('jo');

```
as is^ will not work, name will be undefined. Although, putting `name` as argument in the returns functions in `catchErrors` would output correctly it is not an efficient/ flexible option. Instead, using `...rest` and `...spread` would keep it flexible as it would take whatever amount of arguments one would decide to use

```
function catchErrors(fn) {
  return function(...args) {
    return fn(...args).catch((err) => { 
      console.error(Error(`whoooa -> ${err}`))
    });
  }
}

```
using rest `...args` in first returned function captures all arguments in an array. Then, with spread `...args` in second return to spread all arguments into that function.

put together (with added argument to show flexibility):
```
function breath(amount) {
  return new Promise((resolve, reject) => {
    if (amount < 500) {
      reject('too small of a value');
    }
    setTimeout(() => resolve(`${amount} ms done`), amount);
  })
}

// fn is any function, such as something like -> .map(function(){ })
function catchErrors(fn) {
  return function(...args) {
    return fn(...args).catch((err) => { 
      console.error(Error(`whoooa -> ${err}`))
    });
  }
}

async function go(name1, name2, name3) {
  console.log(`Hey, ${name1}, ${name2}, ${name3}! It's starting...`);
  const res = await breath(1000);
  console.log(res);
  const res2 = await breath(5000);
  console.log(res2);
  const res3 = await breath(300);
  console.log(res3);
  console.log('end');
}

// go(); instead of this
const wrappedFn = catchErrors(go);

wrappedFn('jo', 'enigma', 'scrappy');

```
1 arg, 3 or whatever... doesn't matter. The rest and spread adjust to the number of arg without having to adjust the catchErrors function with those same number of args  and THAT... is pretty damn awesome :D

Note: as snazzy as this was it shouldn't be something used ALL the time because there are cases where you would want to catch the errors inside your function to specifically handle it a certain way.

ex: catching a form validation error would be handled differently than when encountering another type of error. 

above snippet/example is good for use case where you want to handle all errors in similar fashion w/o multiple try/catch errors.