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
  
