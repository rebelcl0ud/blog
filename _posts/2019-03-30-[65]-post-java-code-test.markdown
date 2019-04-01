---
layout: post
title: "Post Java Code Test"
date: 2019-03-30
categories: [java, junit]
---

These random notes deserve their own post taken *post* previous... post? *Annnnnnd how many times can I use 'post' in this sentence?* Sections below were moved from [Code Test In... Java?](https://rebelcl0ud.github.io/blog/java/junit/2019/02/14/62-code-test-in-java.html). Wanted to keep initial post intact and use this as an extension of sorts-- list nuggets I come across as I get a bit more acquainted with Java.

- - - 

On another note, the whole [Eclipse](https://www.eclipse.org/downloads/) usage did intrigue me so I downloaded it. It has a "code completion" feature that you can bring up using the shortcut `ctrl-space`. I needed to change it to something else and found this [gem](https://www.stefaanlippens.net/code_completion_shortcut_eclipse_osx/) explaining how to do just that.

- - - 
I'm totally going to have to start another post for more post-java code challenge stuff, but until then...

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

  - Something that I sorta touched on up there when mentioning casting is the whole container size type bit; numeric primitives and fixed number of bits
	
	- byte(8)
	- short(16)
	- int(32)
	- long(64)
	
	- float(32)
	- double(64)
	
	Note: with floats, ie: 55.5f; placing 'f' prevents it being taken as a double.
	
  - A method uses parameters. A caller passes arguments.
  
  - *Converting a String to an integer?* ie: `int thisWillHoldIntegerNow = Integer.parseInt(StringToConvertToIntGoesHere);`
