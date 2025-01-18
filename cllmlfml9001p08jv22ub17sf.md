---
title: "Intersection Observer | Creating infinite scroll in your web application"
seoTitle: "Intersection Observer | Creating infinite scroll in your web applicati"
seoDescription: "How to Create infinite scrolling effect in web application using Javascript's Interection Observer API"
datePublished: Tue Aug 22 2023 17:42:11 GMT+0000 (Coordinated Universal Time)
cuid: cllmlfml9001p08jv22ub17sf
slug: intersection-observer-creating-infinite-scroll-in-your-web-application
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692726036942/57881ec9-f0fe-4a4b-a811-3e312ec365b2.png
tags: javascript, web-development, reactjs, html5, frontend-development

---

If you're not a cave-dweller and don't harbour a hatred for Jeff Bezos (even if you do, it doesn't matter), you've likely shopped online. When you search for an item on these online stores, you're presented with a list of results. If you're not as peculiar as I am, searching for something like "tiger tooth soaked in human blood," which is highly specific, there's a good chance your search query will yield thousands of products. Do you think your browser loads all 1,000+ items at once? No, that would be too much data for the browser to handle and calculate the user interface. However, as you continue to reach the end of your results, more items keep appearing. This is called an infinite scroll.

Here is an example of the infinite scroll on the YouTube homepage.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692725043561/9e88c776-3f24-4052-8b11-5c2f3ae53637.gif align="center")

There are several techniques to achieve this using JavaScript, but the most efficient one involves using a handy web API called the IntersectionObserver. Let's see how to use this API to implement a mini infinite scrollable list of our own.

The concept involves observing an HTML element every time it comes into the viewport and then triggering a callback. Here's how to create this observer:

Let's create an HTML file that looks like this.

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Infinte Scroll</title>
</head>
<style>
    .product {
        padding: 20px;
        border: 1px solid black;
        margin-bottom: 20px;
        opacity: 0;
        margin-left: 100px;
        transition: all 300ms;
    }
    .visible {
        opacity: 1;
        margin-left: 0px;
    }
</style>
<body>
    <div id="container">
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
        <div class="product">Product</div>
    </div>

    <script src="./index.js"></script>
</body>
</html>
```

Here, we have a list of product cards that are hidden by default (notice the "opacity: 0;" inside the style tag). We also have a script tag pointing to index.js. Now, let's create this index.js.

First, let's obtain all the product cards by their class name.  

```javascript
const cards = document.querySelectorAll('.product');
```

Now let’s create an instance of intersection observer.

```javascript
const productCards= document.querySelectorAll('.product');

const observer = new IntersectionObserver((entries) => {
    // Todo
}, {
    threshold: 0.95,
});

productCards.forEach((card) => {
  observer.observe(card);
});
```

The constructor of this IntersectionObserver class takes two parameters. First parameter is a callback which itself has parameter *entries.* **entries here represent all the items this observer will be observing.** In this case, each entry will contain a product card.

Another parameter in the constructor is an object. This object signifies the options for this particular observer. In this case, we only have a *threshold.* threshold here is a number which **can take any value from 0 to 1.** This signifies the percentage of the item we are observing that should be visible in the viewport for it to be considered **intersecting.** we have given it a value of 0.95 which means when 95% of any product card will come in the viewport, that card will be considered intersecting with the viewport.

Let’s go back to our *index.html* file. We also have another style class *visible,* defined in the styled tag. This style, when applied to our product card, will make the card visible again with a little animation (*transition* property).

Let’s make changes to our observer such that, all the product cards which are at least 95% in the viewport will be visible and the rest will be hidden.

```javascript
const productCards = document.querySelectorAll('.product');

const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        entry.target.classList.toggle('visible', entry.isIntersecting);
    })
}, {
    threshold: 0.95
});

productCards.forEach((card) => {
    observer.observe(card);
});
```

This is what it looks like in action.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692725388764/dc5fdb40-c70a-4c8f-a64e-76be5406a3fd.gif align="center")

There is one catch though. When we scroll up, because we have a logic to toggle the *visible* class when the item is intersecting, it also removes this class when it’s not. So, when we scroll up, we see our cards disappearing from the top. To fix this, we will stop observing the cards which have already intersected.

```javascript
const productCards = document.querySelectorAll('.product');

const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        entry.target.classList.toggle('visible', entry.isIntersecting);
        // unobserving entries which have already intersected
        if (entry.isIntersecting) observer.unobserve(entry.target);
    })
}, {
    threshold: 0.95
});

productCards.forEach((card) => {
    observer.observe(card);
});
```

Okay then! so far what we have is…**nothing.** It’s not even close to infinite scrolling. we are not loading new cards when we reach the end of the scroll. But we did it to learn the basics of intersection observer. Let’s now turn this into an actual infinite scroll card list.

First, we will create another observer which will just observe the last card.

```javascript
const lastCardObserver = new IntersectionObserver((entries) => {
    const lastCard = entries[0];
    if (!lastCard.isIntersecting) return;
    loadMoreCards();
    lastCardObserver.unobserve(lastCard.target);
    lastCardObserver.observe(document.querySelector('.product:last-child'));
}, {
    threshold: 0.95
});

lastCardObserver.observe(document.querySelector('.product:last-child'));
```

Here, as we are observing only one card, we will have just one item in the *entries* array. When this card intersects with the viewport, we will load few more cards. After that, we will unobserve the “last last card” and start observing the “new last card”. Let’s now look at the function *loadMoreCards.*

```javascript
function loadMoreCards() {
    const container = document.getElementById('container');
    for (let i = 0; i < 10; i++) {
        const element = document.createElement('div');
        element.classList.add('product');
        element.innerText = 'Product';
        observer.observe(element);
        container.appendChild(element);
    }
}
```

Here, we are creating 10 new cards and observing them with our original observer. In the end, we are adding these cards to the container.

This is how it looks now!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692725633703/686f8526-fc33-4727-9449-712464f39fbd.gif align="center")

**Perfect Infinite Scroll !**

Now, in real-world applications, instead of loading more cards we will fetch new data using API.

---

> ***Follow me on*** [***twitter***](https://twitter.com/devcodesthings) ***to stay in touch. You can find my writings at*** [***devshekhawat.com***](http://devshekhawat.com)***. Also, subscribe to the newsletter here to get daily updates on 💻 web development, ☀️ life and 📚 productivity.***