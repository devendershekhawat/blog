---
title: "Getting Started with Zustand"
datePublished: Sat May 25 2024 09:04:31 GMT+0000 (Coordinated Universal Time)
cuid: clwlvwuic00180amjevjv6ebl
slug: getting-started-with-zustand
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1716627690110/e0c6303c-f078-4fda-8bdc-73cd9cf6d515.jpeg
tags: tutorial, programming-blogs, javascript, web-development, reactjs

---

Hey there, React developer! If you’ve been wrangling with state management in your React applications, you've probably come across libraries like Redux, MobX, and Context API. While these are powerful tools, they can sometimes feel like overkill for simpler projects. Enter Zustand, a lightweight and intuitive state management library that might just be the perfect fit for your next project. Let's dive in and see what Zustand is all about!

## **What is Zustand?**

Zustand (pronounced "zoosh-tand") is a state management library for React that offers a minimalistic and flexible API. It provides a simpler alternative to Redux and other state management solutions by focusing on ease of use and performance. Zustand's name means "state" in German, and it lives up to its name by providing a clean and straightforward way to manage state in your React applications.

## **Why Choose Zustand?**

Here are a few reasons why Zustand has been gaining popularity among React developers:

1. **Simplicity**: Zustand's API is minimal and easy to learn. You can get started quickly without a steep learning curve.
    
2. **No Boilerplate**: Unlike Redux, which often requires a lot of setup and boilerplate code, Zustand lets you define state and actions in a more concise manner.
    
3. **Performance**: Zustand uses a global store but is optimized for performance. It only re-renders components that actually need to change.
    
4. **Flexibility**: Zustand works seamlessly with other React tools and libraries. Whether you’re using hooks, context, or even other state management libraries, Zustand can fit right in.
    

## **Setting Up Zustand**

Getting started with Zustand is a breeze. First, you'll need to install it:

```bash
npm install zustand
```

or, if you prefer yarn:

```bash
yarn add zustand
```

## **Creating Your First Store**

With Zustand, you create a store using the `create` function. Let’s walk through an example of setting up a simple counter:

### **1\. Create the Store**

```javascript
import create from 'zustand';

const useStore = create(set => ({
  count: 0,
  increment: () => set(state => ({ count: state.count + 1 })),
  decrement: () => set(state => ({ count: state.count - 1 }))
}));
```

Here’s what’s happening:

* `create` is used to define the store.
    
* The `set` function is used to update the state.
    
* `count` is our state variable.
    
* `increment` and `decrement` are actions that modify the state.
    

### **2\. Using the Store in Components**

Now, let’s use this store in two different React components to demonstrate state sharing:

#### **CounterDisplay Component**

```javascript
import React from 'react';
import { useStore } from './store';

const CounterDisplay = () => {
  const count = useStore(state => state.count);

  return (
    <div>
      <h1>Count: {count}</h1>
    </div>
  );
};

export default CounterDisplay;
```

#### **CounterControls Component**

```javascript
import React from 'react';
import { useStore } from './store';

const CounterControls = () => {
  const increment = useStore(state => state.increment);
  const decrement = useStore(state => state.decrement);

  return (
    <div>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
    </div>
  );
};

export default CounterControls;
```

### **3\. Combining Components in App**

Now, let’s use both components in our `App` component:

```javascript
import React from 'react';
import CounterDisplay from './CounterDisplay';
import CounterControls from './CounterControls';

const App = () => {
  return (
    <div>
      <CounterDisplay />
      <CounterControls />
    </div>
  );
};

export default App;
```

### **What's Happening Here?**

1. **State Sharing**: The `useStore` hook allows both `CounterDisplay` and `CounterControls` to access and manipulate the same state. This demonstrates how Zustand can be used for state sharing across multiple components.
    
2. **Reactivity**: When you click the increment or decrement buttons in `CounterControls`, the `count` state updates. This triggers a re-render in the `CounterDisplay` component, reflecting the new count value.
    

## **Advanced Usage**

Zustand is powerful and can handle more complex state management needs. Here are a few advanced features:

### **Middleware**

Zustand supports middleware to enhance your store. For example, you can add logging to see state changes:

```javascript
import create from 'zustand';
import { devtools } from 'zustand/middleware';

const useStore = create(devtools(set => ({
  count: 0,
  increment: () => set(state => ({ count: state.count + 1 })),
  decrement: () => set(state => ({ count: state.count - 1 }))
})));
```

### **Persisting State**

You can persist your state to local storage or other storage solutions using middleware:

```javascript
import create from 'zustand';
import { persist } from 'zustand/middleware';

const useStore = create(persist(set => ({
  count: 0,
  increment: () => set(state => ({ count: state.count + 1 })),
  decrement: () => set(state => ({ count: state.count - 1 }))
}), {
  name: 'counter-storage' // name of the item in storage
}));
```

## **Conclusion**

Zustand offers a fresh and simple approach to state management in React. Its minimalistic API, combined with powerful features, makes it a great choice for both small projects and more complex applications. Whether you're tired of the boilerplate in Redux or looking for a more performant alternative to Context API, give Zustand a try. Happy coding!

***Follow me on***[***t witter***](https://twitter.com/dev_is_a_dev)***to stay in touch. Also, subscribe to the newsletter to get daily updates on 💻 web development, ☀️ life and 📚 productivity.***