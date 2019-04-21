---
layout: post
title: "Head First Java"
date: 2019-03-30
categories: [java, junit]
---

These random notes deserve their own post taken *post* previous... post? *Annnnnnd how many times can I use 'post' in this sentence?* Sections below were moved from [Code Test In... Java?](https://rebelcl0ud.github.io/blog/java/junit/2019/02/14/62-code-test-in-java.html). Wanted to keep initial post intact and use this as an extension of sorts-- list nuggets I come across as I get a bit more acquainted with Java.

- - -
Eclipse:

On another note, the whole [Eclipse](https://www.eclipse.org/downloads/) usage did intrigue me so I downloaded it. It has a "code completion" feature that you can bring up using the shortcut `ctrl-space`. I needed to change it to something else and found this [gem](https://www.stefaanlippens.net/code_completion_shortcut_eclipse_osx/) explaining how to do just that.

- - -
Head First Java:

Some of this stuff is not completely foreign, I see similarities with JavaScript, however there is info presented I may or may not have come across at some point, but *suprise* don't remember-- going through 'Head First Java', if I find something interesting or didn't know it's going here.

  - Don't forget to import stuff. *What does that mean?* Well, I was messing with Arrays and I wanted to print out to console... you're not gonna get anywhere if it doesn't know wth you're talking about. `import java.util.Arrays;` tossing this onto the top of the file got it done.

Speaking of printing out Arrays--
```
import java.util.Arrays; 

class Practice {
	
	public static void main(String[] args) {
		int[] nums;

		nums = new int[7];
		
		System.out.println(nums);
	}
}
```
That^ outputs `[I@677327b6`. To get `[0, 0, 0, 0, 0, 0, 0]` => `System.out.println(Arrays.toString(nums));`

  - Something that I sorta touched on up there when mentioning casting is the whole container size type bit; numeric **primitives** and fixed number of bits
	
	- byte(8)
	- short(16)
	- int(32)
	- long(64)
	
	- float(32)
	- double(64)
	
	Note: with floats, ie: 55.5f; placing 'f' prevents it being taken as a double.
	
  - A method uses parameters. A caller passes arguments.
  
  - *Converting a String to an integer?* ie: `int thisWillHoldIntegerNow = Integer.parseInt(StringToConvertToIntGoesHere);`
  
  - `x++` vs. `++x`; affects result-- placement determines whether to increment first or after using the value of `x`.
  
  - `for` vs. `while` loop: if you know number of iteration use a for, else use while to run while a condition is true. I think I've rarely use while loops, but this is a good way to think about usage. Speaking of `for` loops: `for(String name : nameArray){}` (the enhanced for loop) reads as if it were a `for each` or `for in` loop. Note: variable declared to hold single element of array as it iterates, the variable type, must be compatible with elements inside array.
  
  - `Arrays` can't change in size. A new array would need to be created to copy over remaining elements from old array. An `ArrayList` however grows/shrinks when elements are added/removed; no need to iterate through just ask if element is contained.
  
  - Some `ArrayList` can-dos: `.add()`, `.size()`, `contains()`, `indexOf()`, `isEmpty()`, `.remove()`
  
  - *I had no idea this was a thing* `&` and `|`, non short circuit operators. They act like their counterparts, `&&` and `||` except they force to have both sides of the expression checked. In comparison, the `&&` and `||` doesn't bother to check the right side if left side of expression shows false or true (respectively).
  
  - - - 
  
  
Below started as a section within Design Patterns post, but it started looking like this could get a bit longer so it was moved here. Design Patterns will be left solely for notes on the design playlist as was the initial intent. What follows are 'notes' as I make my way through the Head First Java book. sn: *I miss JavaScript and hope I don't forget it as I delve deeper into Java.*

## inheritance check 
  Something I've come across in relation to design patterns; OO
  
  A good way to keep your inheritance in check when designing is using `IS-A`. Example: Dog `is-a` Canine `is-a` Animal. Note: `is-a` relationship works in only 1 direction.
  
## access levels
  
  Access Levels: `public` instance variables/ methods are not inherited, `private`are not. There are also `default` and `protected`.
  
## super
  Subclass using super class method and subclass override method: use `super.addMethodHereLikeSleep()` followed by your own method that way it runs both.
  ```
  puublic void sleep() {
    super.sleep();
    // the override follows here
  }
  ```
## polymorphism 
  *Polymorphism*-- when definining a supertype for a group of classes, any of the subclasses (of that supertype) can be used where the supertype is expected.
  
  **Car myCar** = new Car(); // create instance variable
  
  Car myCar = **new Car();** // create object
  
  Car myCar **=** new Car(); // make the relation; connect instance variable to object, typical creation-- both types match, both are of type Car.
  
  With *polymorphism*: **Vehicle** myCar = new Car(); // the reference and object can differ
  
  ### override & overload
  Speaking of *polymorphism*-- for it to work and **override** super class method-- **arguments must be the same & have compatible return types**. The compiler will look at reference types to decided whether or not to give you the go ahead to call method on that reference. Given the compiler gives the greenlight, at runtime JVM doesn't look at reference type but at the actual object on the heap you are calling method on. Note: to override though arguments must be the same and have compatible return types, as well as the method cannot be less accessible.
  
  One the flip side, you can **overload** a method, but that doesn't involve polymorphism. **Two methods by the same name with *different* arguments lists-- return types may be different, but return type cannot be the *only* change.** Note: You can also vary access levels, ie: overload a method with a more restrictive method.
  
  ### `ArrayList<Object>`
  Instead of making an ArrayList of specific vehicles, you are able to make one of Vehicles where it would take in different types of vehicles. Coming out of the ArrayList however, they'd be of type Object-- the way to revert back to its correct type would be through *casting*.
  
  ```
  Object o = theArrayList.get(index);
  Car c = (Car) o;
  c.drive();
  ```
  Checking type...
  ```
  if(o instanceof Car) {
    Car c = (Car) o;
  }
  ```
  will prevent a `ClassCastException` at runtime.
  
  ### abstract
  Purpose of an abstract class is to be *extended*; abstract methods must be *overridden*. An abstract method has no body and if you declare a method abstract, you **must** mark the class abstract as well. However, you can mix both abstract and non-abstract methods in the abstract class.
  
  *What's the point of an abstract method?* While you haven't placed in actual code, you've defined part of protocol for a group of subclasses(subtypes). You want the ability to use a superclass type(often abstract) as a method argument, return type, or array type.
  
  An example of this would be adding subclasses to a superclass like Animal-- having Animal go in as an argument for a method within a Vet class prevents writing out seperate methods for any/ every type of Animal.
  
  **Implementing an abstract method is like overriding a method**
  Abstract methods have no body, they exist solely for polymorphism leaving the first concrete subclass down the inheritance tree to implement *all* abstract methods. Implement, meaning provide the method a body-- a non-abstract method with the same structure of name/arguments/return type. What you put in it is all on you, Java cares only that exists in the concrete class.
  
  ### interface
  To avoid multiple inheritance use interface. When *defining* an interface, ie: `public interface Supercharged {...}`; And when *implement*ing, ie: `public class Civic extends Car implements Supercharged {...}`.
  
  Some things about an interface: they are like 100% abstract class, when you implement you can still extend class, methods end in semicolons, methods from interface must be used in (if continuing with example) Civic class which satisfies the first concrete class having to implement abstract method inherited down the tree. 
  
  Note: a class can implement multiple interfaces, ie: `public class Dog extends Animal implements Pet, ServiceAnimal, Therapy {...}`
  
 ## When to use what? [class, subclass, abstract class, interface]
 
  - Make a class that doesn't extend anything when there is no `is-a`.
  
  - Subclass to extend a class for more specific behavior derived from class-- override or add new behavior.
  
  - Use an abstract class to define a type of "template" for a group of subclasses and use some implemented code for all subclasses to use. Also, if you don't want anyone making an object of the type abstract is a good way to go.
  
  - Use an interface to define a *role* that other classes may play regardless of where they are in the inheritance totem pole.
  
 ## Objects and their *cues music* "circle of life"
 
 ### Heap & Stack
 Two areas of memory-- the **heap**, *where objects live* and the the **stack**, *where the invoke of methods and local variables live*.
 
 **Instance variables are declared within a class, not a method**-- they represent 'fields' a object has and are able to hold values for different instances of objects created from its class. They live within the object they belong to and therefore also reside in the heap.
 
 **Local variables (aka stack variables) are declared within a method (including method parameters)**-- they live as long as the method that created them lives *on the stack*, ie: as soon as that last curly brace hits *poof*.
  
