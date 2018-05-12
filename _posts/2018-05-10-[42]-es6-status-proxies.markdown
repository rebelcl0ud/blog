---
layout: post
title: ES6 Status - Proxies
date: 2018-05-10
categories: javascript
---
Proxies allow you to override default behavior for many of Object's default operations-- there are a multitude of methods that come as Object default.

`const pup = { name: 'enigma', age: 12 };`

if I wanted to return something other than 'enigma'...

`const pupProxy = new Proxy(object youd like to proxy goes here, {
  handler goes here- where you specify operations looking to rewrite
});`

[Proxy/handler](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler)

overriding operation/ inside handler is called traps-- what sits between you and object.

```
const pup = { name: 'enigma', age: 12 };
const pupProxy = new Proxy(pup, {
	
});
```
`pupProxy.name = 'enigmatic';` sets property of name on pupProxy, to trap that from happening-- go in the middle of implementing logic for set.

```
const pup = { name: 'enigma', age: 12 };
const pupProxy = new Proxy(pup, {
  get(target, name) {
    console.log('asking for ', target, name);
  }	
});

pupProxy.name = 'enigmatic';

```

console output gist:
```
>>pupProxy
    Proxy
    ​
      <target>: {…}
      ​​
        age: 12
        ​​
        name: "enigmatic"
        ​​
        <prototype>: Object { … }
      ​
      <handler>: {…}
      ​​
        get: get()
        ​​​
          length: 2
          ​​​
          name: "get"
          ​​​
          <prototype>: function ()
          ​​
        <prototype>: Object { … }
>>pupProxy.name
  asking for  Object { name: "enigmatic", age: 12 } name

```
^console.logs entire object and key => name

```
const pup = { name: 'enigma', age: 12 };
const pupProxy = new Proxy(pup, {
  get(target, name) {
    // console.log('asking for ', target, name);
    return 'hijacked'
  } 
});

pupProxy.name = 'enigmatic';

```
^return shows example of jumping in the middle of the `get()` possible usage is to modify or checks, such as `toUpperCase()`

```
const pup = { name: 'enigma', age: 12 };
const pupProxy = new Proxy(pup, {
  get(target, name) {
    // console.log('asking for ', target, name);
    return `hijacked`.toUpperCase();
  },
  set(target, name, value) {
    if(typeof value === 'string') {
      target[name] = value.trim();
    }
  }
});

pupProxy.name = 'enigmatic';

```

console output gist, adding set:

`pupProxy.whut = '    check out all this useless space   '`

outputs this `"    check out all this useless space   "`

however, input of `pupProxy` in console outputs `whut` tidy and trimmed as `set` in snippet above^. 
```
>>pupProxy
  Proxy
    <target>: {…}
    ​​
      age: 12
      ​​
      name: "enigmatic"
      ​​
      whut: "check out all this useless space"
      ​​
      <prototype>: Object { … }
    ​
    <handler>: Object { … }
```

Note: if you don't specify one of listed traps, [Proxy/handler](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler), object default will take over.

