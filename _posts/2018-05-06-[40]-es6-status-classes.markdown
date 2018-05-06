---
layout: post
title: ES6 Status - Classes
date: 2018-05-06
categories: javascript
---

Prototypal Inheritance

```
function Dog(name, breed) {
	this.name = name;
	this.breed = breed;
}

const scrappy = new Dog('Scrappy', 'mixed')

```

Note: Dog is capitilized because it is a constructor.

*What is protypal inheritance?* When you put a method on the original constructor it will be inherited.

Example: when you create an array, `const turtles = [leo, raph, donnie, mikey]` turles will now have methods available to use, such as `join()`

*Where did that come from?* `Array`, queen bee, that if you look inside comtains a multitude of prototype methods. Which means when you create an array every instance created inherits those methods.

Or, like above example you create a dog, from Dog (which in this case would be the queen bee)

Note: they don't take their own, but share

```
Dog.prototype.bark = function() {
	console.log(`Rrrrruufffff! I'm ${this.name}`);
}

```
typing `scrappy.bark()` should output `Rrrrruufffff! I'm Scrappy` in console.

Now, making 2nd dog...
`const enigma = new Dog('Enigma', 'Lab mix')`

return `Rrrrruufffff! I'm Enigma` in console using bark method as well `enigma.bark()`

In other words, the bark method which was added to queen bee Dog is inherited by every instance created like with scrappy and enigma example above.

Note:
	- you are able to override methods such as bark even after creating the instance
	- you can add another method to prototype after creating instance 
	- when you console.log an instance, ex: scrappy, opening it up in console you'll see name and breed, which are specific to the instance, but to see prototype methods-- those are located under proto which are inherited methods from parent, they are not part of the actual object of scrappy itself.

