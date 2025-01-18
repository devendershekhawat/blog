---
title: "Proxies and traps in Javascript: What & Why"
seoTitle: "Proxies and traps in Javascript"
seoDescription: "In Javascript, a proxy acts as an intermediary between the code and an object. It allows developers to intercept fundamental operations on an object."
datePublished: Sat Aug 12 2023 08:54:25 GMT+0000 (Coordinated Universal Time)
cuid: cll7s6e8e000509l4g3cheme5
slug: proxies-and-traps-in-javascript-what-why
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692000442830/db20f678-1fb8-4f1e-8f95-4886864fc701.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1692000469005/e9c08392-a058-4357-b53c-b175246c78cb.png
tags: javascript, web-development, reactjs, frontend-development, vanilla-js-1

---

In Javascript, everything is an Object. And, these objects have some fundamental operations like getting and setting a value.

```javascript
const student = {
    rollNo: 123,
    firstName: 'Dev',
    lastName: 'Shekhawat',
    marks: '68',
    maximumMarks: '100'
}

//getting a value
console.log(student.firstName);
//setting a value
console.log(student.lastName);
```

But, what if you want to perform some internal operations when a value in an object is accessed or is assigned a new value? Let's take a simple example. Suppose, whenever any property of the `student` object is accessed, you want to log who accessed what property to the analytics.

How will you implement this without creating a custom function like `getProperty(object, property)` and by just calling `student.firstName` or any other property of the `student` object. The answer is **Proxies**.

### What are proxies?

In the world of JavaScript, where flexibility and dynamism reign supreme, developers are constantly seeking ways to achieve more powerful and efficient code. One such tool that has gained prominence over the years is the concept of "proxies." Proxies are a versatile and advanced feature of JavaScript that allows developers to intercept and customize fundamental operations on objects, enabling a whole new level of metaprogramming and control.

a proxy acts as an intermediary between the code and an object. It allows developers to intercept and customize the fundamental operations on the target object, such as property access, assignment, deletion, function invocation, and more. Proxies essentially enable you to redefine the default behaviour of object operations, granting you unprecedented control over the interactions with your objects.

### Creating a proxy.

To create a Proxy, we use the `Proxy` constructor, passing in the target object (the object you want to wrap with the Proxy) and a handler object that defines the custom behaviour for intercepted operations. The handler object contains methods, known as `traps`, that get invoked when corresponding operations are performed on the Proxy.

Creating a proxy to override property access on the `student` object.

```javascript
const student = {
    rollNo: 123,
    firstName: 'Dev',
    lastName: 'Shekhawat',
    marks: '68',
    maximumMarks: '100'
}

const handler = {
    get: function(target, property) {
        analytics.log(`property ${property} accessed by ${window.user}`)
        return target[property];
    },
};

const studentProxy = new Proxy(studentProxy, handler);

console.log(studentProxy.marks);

// Logger: property marks accessed by Dev
// 68
```

In this example, the `get` trap intercepts property access on the proxy. It logs the accessed property and username to analytics and returns the value.

Let's build another feature where, whenever the marks of a student are updated, we log the data to analytics and recalculate the percentage and vice versa.

```javascript
const student = {
    rollNo: 123,
    firstName: 'Dev',
    lastName: 'Shekhawat',
    marks: '68',
    maximumMarks: '200',
    percentage: '34'
}

const handler = {
    get: function(target, property) {
        analytics.log(`property ${property} accessed by ${window.user}`)
        return target[property];
    },
    set: function(target, property, value) {
        analytics.log(`property ${property} changed by ${window.user} from ${target[property]} to ${value}`);
        target[property] = value;        
        if (property === 'marks') {
            target.percentage = (value/target.maximumMarks) * 100;
        }
        if (property === 'percentage') {
            target.marks = (value * target.maximumMarks)/100;
        }
        return true;
    },
};

function recalculatePercan

const studentProxy = new Proxy(studentProxy, handler);

student.marks = 100;
// Logger: property marks changes by Dev from 68 to 100
```

In this example, the `set` trap intercepts property assignment on the proxy. It logs the assignment and then sets the percentage if the property is `marks` or vice versa.

Proxies can also be created for function invocation.

### Proxying function invocation.

```javascript
const targetObject = {
    add: function(a, b) {
        return a + b;
    },
};

const handler = {
    apply: function(target, thisArg, argumentsList) {
        console.log(`Calling function: ${target.name}`);
        return target.apply(thisArg, argumentsList);
    },
};

const proxy = new Proxy(targetObject.add, handler);

console.log(proxy(5, 3)); // Calling function: add | Output: 8
```

In this example, the `apply` trap intercepts function invocation on the proxy. It logs the function call and then invokes the corresponding function on the target object.

Other possible `traps` or operations that you can intercept using proxies are (but not limited to):

1. `has` Trap: This trap intercepts the use of the `in` operator to check for the existence of properties in an object.
    
2. `deleteProperty` Trap: This trap intercepts property deletion using the `delete` operator.
    
3. `construct` Trap: This trap intercepts the creation of instances using the `new` keyword.
    
4. `getOwnPropertyDescriptor` Trap: This trap intercepts calls to `Object.getOwnPropertyDescriptor()`.
    
5. `getPrototypeOf` Trap: This trap intercepts calls to `Object.getPrototypeOf()`.
    

These are just a few examples of the traps available in JavaScript Proxies. Each trap allows you to customize a specific aspect of an object's behaviour, enabling you to create tailored interactions and behaviours based on your application's needs. When using proxies, keep in mind that proper handling of the traps is essential to ensure the correct behaviour and performance of your code.

**Conclusion**

JavaScript Proxies offer a powerful way to customize the behaviour of objects flexibly and dynamically. By intercepting and handling fundamental operations, proxies enable developers to implement features such as logging, validation, access control, and more. They provide an elegant solution for achieving advanced object manipulation without modifying the original object's structure.

While proxies are a powerful tool, it's important to use them judiciously. Excessive use of proxies can lead to code complexity and reduced performance. However, when used wisely, proxies can elevate your JavaScript code to new levels of abstraction and versatility.

---

> Follow me on [twitter](https://twitter.com/devcodesthings) to stay in touch 👋🏼. Subscribe to my newletter **A Damn Good Developer** [here](https://damngooddev.beehiiv.com/subscribe) to get daily updates on web development 💻, developer lifestyle 🤓and productivity 📚.

%%[beehiiv]