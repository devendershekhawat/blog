---
title: "How cleanup works in React's useEffect hook"
seoTitle: "How cleanup works in React's useEffect hook"
seoDescription: "clean up resources or subscriptions in your React Component to prevent memory leaks or unexpected behaviour."
datePublished: Thu Aug 17 2023 13:47:52 GMT+0000 (Coordinated Universal Time)
cuid: cllf7v104000109ma1dyr4rvt
slug: how-cleanup-works-in-reacts-useeffect-hook
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692278842194/436ed754-7675-41e2-a27f-55c15f3549a4.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1692280048809/7ca1d394-5ea7-4f8f-9540-dfb80c02e770.png
tags: javascript, web-development, reactjs, html5, frontend-development

---

In React, the `useEffect` hook is used to manage side effects in functional components of React. It allows you to perform operations such as data fetching, DOM manipulation, or subscriptions.

At the basic level, the syntax of `useEffect` looks something like this.

```javascript
useEffect(callback, [...dependencies]);
```

The dependencies array contains a list of variables, and whenever these variables change, the callback executes.

A basic example of `useEffect` within an actual React component may appear as follows.

```javascript
// JavaScript (React)

import React, { useState, useEffect } from 'react';

function ExampleComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // This code runs whenever the 'count' state changes
    console.log('Count has changed:', count);
  }, [count]); // Dependency array: useEffect will only run when 'count' changes

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase count</button>
    </div>
  );
}

export default ExampleComponent;
```

Here, the dependencies array has only one variable, the `count` state. Whenever this `count` changes the first argument of useEffect, i.e. the callback executes and we get `Count has changed:` logged in the console.

There are two more points worthy of note about the `useEffect` hook,

1. When the dependencies array is not provided, the callback or the effect runs on every render.
    
2. When the dependencies array is empty `[]`, the effect run only when the component mounts.
    

### The cleanup

Sometimes, the callback in `useEffect` return "another function". This function is called the `cleanup`.

```javascript
useEffect(() => {
    // This code runs whenever the 'count' state changes
    console.log('Count has changed:', count);

    return () => {
        console.log('The count was updated');
    }
  }, [count]); // Dependency array: useEffect will only run when 'count'
```

The cleanup function runs whenever the component unmounts or before executing the effect again due to dependency changes. It "cleans up" the effect of the previous value dependency before running the effect once more.

Let's consider a real-world example where you're building a chat application using React. In this scenario, you might use the `useEffect` hook to establish a connection to a chat server and subscribe to new messages. You'll want to clean up the subscription when the component unmounts or when the user switches to a different chat room.

Here's how the code might look:  

```javascript
import React, { useState, useEffect } from 'react';
import ChatService from './ChatService'; // Hypothetical chat service module

function ChatRoom({ roomId }) {
  const [messages, setMessages] = useState([]);

  useEffect(() => {
    // Establish a connection to the chat server and subscribe to messages
    const subscription = ChatService.subscribeToRoom(roomId, (newMessage) => {
      setMessages((prevMessages) => [...prevMessages, newMessage]);
    });

    // Return the cleanup function
    return () => {
      // Unsubscribe from the chat room when the component unmounts
      ChatService.unsubscribeFromRoom(subscription);
    };
  }, [roomId]);

  return (
    <div>
      <h2>Chat Room {roomId}</h2>
      <ul>
        {messages.map((message, index) => (
          <li key={index}>{message.text}</li>
        ))}
      </ul>
    </div>
  );
}

export default ChatRoom;
```

In this example, the `ChatRoom` component subscribes to a chat room using the `ChatService.subscribeToRoom` method. The subscription callback adds new messages to the `messages` state array. The cleanup function ensures that the subscription is removed when the component unmounts, preventing memory leaks and unnecessary network requests.

By using the `useEffect` cleanup mechanism, you ensure that you're not leaving any open connections or resources behind when the component is no longer in use. This approach helps maintain a clean and performant application.

---

> ***Follow me on*** [***twitter***](https://twitter.com/devcodesthings) ***to stay in touch. You can find my writings at*** [***devshekhawat.com***](http://devshekhawat.com)***. Also, subscribe to the newsletter here to get daily updates on 💻 web development, ☀️ life and 📚 productivity.***
> 
> %%[beehiiv]