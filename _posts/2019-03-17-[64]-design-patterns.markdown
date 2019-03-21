---
layout: post
title:  "Design Patterns"
date:   2019-03-19
categories: design patterns
---

Since turning in my Java code challenge I've been familiarizing myself with design patterns. I came across a pretty helpful YouTube channel that I will have to link in here soon--

3 categories: Creational, Behavorial, Structural

`Creational Patterns` I came across: Strategy, Observer, Factory, Abstract, Singleton, Builder, Prototype.

`Strategy Pattern` lets algorithms vary independently from clients that use it; define a family of algorithms, encapsulate each one, make them interchangeable.

`Observer Pattern`: object called subject maintains a list of dependents called observers and notifies them automatically of any state changes, usually by calling one of their methods.

`Factory Pattern`: allows you to create objects without specifying the exact class of object that will be created.

`Abstract Factory Pattern`: similar to factory, except everything is encapsulated.
  - methods that order objects
  - factories that build objects
  - final object; final object contains object that uses strategy pattern
  - composition object class fields are object

`Singleton Pattern` is used when you want to eliminate the option of instantiating more than one object

`Builder Pattern`: used to create objects made from a bunch of other objects
  - when you want to build an object from other objects
  - when you want the creation of those parts to be independent of the main object
  - hide the creation of the parts from the client so both aren't dependent
  - the builder knows the specifics and nobody else does

`Prototype Pattern`:
  - creates new objects (instances) by cloning (copying) other objects
  - allows for adding of any subclass instance of a known super class at run time
  - when there are numerous potential classes that you want to only use if needed at run time
  - reduces the need for creating subclasses
