---
layout: post
title: ES6 Status - Map and Weak Map
date: 2018-05-14
categories: javascript
---

Sets are to arrays what map is to objects. Map works similar to sets, but have key and value instead of just values (as with a set).

Able to use `.has()` and `.delete()` like with sets, but unlike sets able to use `.get()` to reference items.

```
const pups = new Map();

pups.set('reese', 2);
pups.set('tuxx', 4);
pups.set('texx', 6);

```

`pups.has('reese')` in console => true
`pups.get('reese')` in console => 2
`pups.delete('reese')` in console => true, `pups` in console then => `Map { tuxx → 4, texx → 6 }`

Able to loop with `for each`:
```
pups.forEach((pupVal, pupKey ) => {
  console.log(pupVal, pupKey)
});

```
which will console:
```
2 reese
4 tuxx
6 texx

```

Able to loop using `for of`:
```
for(const pup of pups) {
  console.log(pup);
}

```
which will console:
An array, first item being key and second item being value.
```
Array [ "reese", 2 ]
Array [ "tuxx", 4 ]
Array [ "texx", 6 ]

```
Using deconstruction:
```
for(const [pupKey, pupVal] of pups) {
  console.log(pupKey, pupVal);
}

```
will console:
```
reese 2
tuxx 4
texx 6

```
*So, why use map instead of object?* metadata
