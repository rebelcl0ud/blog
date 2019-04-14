---
layout: post
title:  "OO & Polymorphism"
date:   2019-04-14
categories: [java, design patterns]
---

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
  
  ### interfaces
  To avoid multiple inheritance use interface. When defining an interface, ie: `public interface Supercharged {...}`; implement `public class Civic extends Car implements Supercharged {...}`.
  
  Some things about an interface: they are like 100% abstract class, when you implement you can still extend class, methods end in semicolons, methods from interface must be used in (if continuing with example) Civic class which satisfies the first concrete class having to implement abstract method inherited down the tree. 
  
  Note: a class can implement multiple interfaces, ie: `public class Dog extends Animal implements Pet, ServiceAnimal, Therapy {...}`
