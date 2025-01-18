---
title: "🚀 Set, Map & WeakMap in Javascript"
seoTitle: "Set, Map & WeakMap in Javascript"
seoDescription: "Ever wondered if you can create objects which has other objects as keys?"
datePublished: Sat Aug 19 2023 10:00:21 GMT+0000 (Coordinated Universal Time)
cuid: cllhum4oq000109lb51jl5yss
slug: set-map-weakmap-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692439586362/b5747f6b-1829-4c7f-b8e6-4ec7adfd4be5.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1692439609888/2a3e9c37-8e3a-4957-94cb-69154f633fac.png
tags: webdevelopment, css, javascript, reactjs, frontend-development

---

Happy Saturday Devs!

Let's start with a beautiful thought that just occurred to me while contemplating about mysteries of life, the universe and coding.

%[https://twitter.com/devcodesthings/status/1692585121734615415] 

Now that it's out of the way, Let's talk some JS!

JavaScript is a super handy and popular programming language that comes with a bunch of data structures to make working with data a breeze. Set, Map, and WeakMap are some cool constructs that give you unique ways to store and organize your data. In this blog, we'll dive into these three data structures and figure out when and how to use them in your JavaScript projects. 😊

### **1\. Set**

A `Set` is a built-in JavaScript data structure that represents a collection of unique values. It can store various data types, such as numbers, strings, objects, and more. The key feature of a `Set` is that it enforces uniqueness, meaning that it will not allow duplicate values. Here's how you can create and use a `Set`:

```javascript
const mySet = new Set();

mySet.add(1);
mySet.add(2);
mySet.add(2); // Duplicate value, will not be added

console.log(mySet); // Set { 1, 2 }
```

**Common** `Set` **Methods**:

* `add(value)`: Adds a value to the `Set` if it doesn't already exist.
    
* `delete(value)`: Removes a value from the `Set`.
    
* `has(value)`: Checks if a value exists in the `Set`.
    
* `size`: Returns the number of elements in the `Set`.
    
* `clear()`: Removes all values from the `Set`.
    

`Set` is particularly useful when you need to store a collection of unique values, such as a list of distinct items or filtering duplicate entries from an array.

### **2\. Map**

A `Map` is another built-in data structure in JavaScript that stores key-value pairs. Unlike regular objects, `Map` allows any data type as keys and maintains the order of insertion. This makes it an excellent choice for scenarios where you need to associate data with specific keys or maintain the order of data insertion. Here's how you can use a `Map`:

```javascript
const myMap = new Map();

myMap.set('name', 'John');
myMap.set('age', 30);

console.log(myMap.get('name')); // John
console.log(myMap.has('email')); // false
```

### 3\. WeakMap

A `WeakMap` is a specialized type of `Map` that allows only objects as keys and holds weak references to these keys. Unlike regular objects or `Map`, `WeakMap` does not prevent the garbage collector from collecting keys that are no longer referenced anywhere else in your program. This makes it useful for scenarios where you want to associate data with objects without preventing those objects from being garbage collected when they are no longer needed. Here's how you can use a `WeakMap`:

```javascript
const myWeakMap = new WeakMap();
const key = {};

myWeakMap.set(key, 'Secret Data');

console.log(myWeakMap.get(key)); // Secret Data

// When key is no longer referenced elsewhere, it can be garbage collected, and its associated data will be automatically removed from the WeakMap.
```

**Common** `WeakMap` **Methods:**

* `set(key, value)`: Sets a key-value pair in the `WeakMap`.
    
* `get(key)`: Retrieves the value associated with a key.
    
* `has(key)`: Checks if a key exists in the `WeakMap`.
    
* `delete(key)`: Removes a key-value pair from the `WeakMap`.
    

`WeakMap` is particularly useful when you need to associate additional data with objects, but you don't want to prevent those objects from being cleaned up by the garbage collector when they're no longer in use.

In summary, `Set` is ideal for maintaining collections of unique values, `Map` is perfect for key-value associations with order preservation, and `WeakMap` is a specialized choice for associating data with objects while allowing those objects to be garbage collected.

Understanding when and how to use these data structures can significantly enhance your JavaScript applications, improving both performance and code clarity. Whether you're working on a simple task or a complex application, having a good grasp of these data structures can be a valuable asset in your JavaScript development toolkit.

> ***Follow me on*** [***twitter***](https://twitter.com/devcodesthings) ***to stay in touch. You can find my writings at*** [***devshekhawat.com***](http://devshekhawat.com)***. Also, subscribe to the newsletter here to get daily updates on 💻 web development, ☀️ life and 📚 productivity.***