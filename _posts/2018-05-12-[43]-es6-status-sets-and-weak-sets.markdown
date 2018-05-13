---
layout: post
title: ES6 Status - Sets and Weak Sets
date: 2018-05-12
categories: javascript
---

A set is like a unique array-- no copies of items, no accessing individual items and not index-based. Set, a list of items able to add to, remove from and loop over.

I.
creating a new set: `const dogs = new Set();`
adding to set: `dogs.add('scrappy');` and so on with additional names.

when you open in browser and type dogs in console, returns set with dog/names inside, `Set(3) [ "scrappy", "flavor", "bandit" ]` 

similar to array, but notable differences shown in dropdowns within console output. such as, with `.size()` similar to `.length()` in arrays.

```
Set(3)
​
	size: 3
	​
	<entries>
	​​
		0: "scrappy"
		​​
		1: "flavor"
		​​
		2: "bandit"
	​
	<prototype>: {…}
	​​
		add: function add()
		​​
		clear: function clear()
		​​
		constructor: function Set()
		​​
		delete: function delete()
		​​
		entries: function entries()
		​​
		forEach: function forEach()
		​​
		has: function has()
		​​
		keys: function values()
		​​
		size: Getter
		​​
		values: function values()
		​​
		Symbol(Symbol.iterator): function values()
		​​
		Symbol(Symbol.toStringTag): "Set"
		​​
		<prototype>: Object { … }

```
to `delete` from set: `dogs.delete('bandit');`, input of dogs in console will return edited set.

to clear set: `dogs.clear();` will remove all items from inside set.

calling `dogs.values()` will output `SetIterator` which gives ability to loop over set and like a generator can call `next()` on it.
```
// console
const whuuut = dog.values()

whut.next(); // console.logs Object { values: "scrappy", done: false }

```
^with each next, value output changes, moving through the list until it is done.

```
for(const dog of dogs) {
	console.log(dog);
}

```
^which will output names in dog set

Note: in SETS, no difference btwn `.keys()` and `.values()`, `.entries()` will show key/values same

II.
can declare a set with values in it/ pass it just like you would an array, `const kids = new Set(['bandit', 'flavor', 'scrappy']);`


can create a set when passing an array...
here's existing array, `const hamsters = ['ernie', 'ozzie', 'tommy'];` that can be passed into new set, `const hamsterSet = new Set(hamsters);`

hamsters input will show array while hamsterSet will show set.

`.has()` can be used to check if set HAS a certain item which will return a true or false.