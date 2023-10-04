---
title: "Unlock the Power of JavaScript WeakSet: Mastering a Hidden Gem!"
datePublished: Wed Oct 04 2023 06:22:01 GMT+0000 (Coordinated Universal Time)
cuid: clnbd2jzh001408mnf6hpgjkk
slug: unlock-the-power-of-javascript-weakset-mastering-a-hidden-gem
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695752493733/53b5c3b1-0221-47dc-b8bd-c40ed10639e6.png
tags: js, javascript, es6, es2015, weakset

---

In the vast landscape of JavaScript, many powerful features often go unnoticed. One such hidden gem is the WeakSet, an unsung hero of the language that can help you optimize your code and manage memory more effectively. In this article, we'll dive deep into WeakSet, uncovering their potential and learning how to use them effectively in our JavaScript projects.

## A Brief Introduction to WeakSet

WeakSet is a collection of objects similar to the more commonly used Set.  
However, there's a significant difference between the two: WeakSet holds only weak references to the objects stored within them. This means that if an object is only referenced by a WeakSet, it can still be garbage collected, freeing up valuable memory resources.

This unique feature of WeakSet makes it an excellent choice for managing certain types of data relationships, mainly when memory management is a priority.

## Creating and Using WeakSet

To create a WeakSet, instantiate a new instance of the WeakSet class:

```javascript
const weakSet = new WeakSet();
```

Adding objects to a WeakSet is easy. Just use the `add` method:

```javascript
const obj1 = {};
const obj2 = {};

weakSet.add(obj1);
weakSet.add(obj2);
```

WeakSets also provide methods for checking if an object is present (`has`) and removing objects (`delete`):

```javascript
console.log(weakSet.has(obj1)); // true
weakSet.delete(obj1);
console.log(weakSet.has(obj1)); // false
```

However, unlike Sets, WeakSets do not have methods for iterating over their contents or determining their size. This is because of their weakly-referenced nature, which makes it impossible to know how many objects are still being held in memory.

## Use Cases for WeakSets

#### 1\. Managing DOM Elements

`WeakSet` can be incredibly useful when working with the DOM. You can store references to DOM elements without worrying about memory leaks. When an element is removed from the DOM, the reference in the `WeakSet` will be automatically garbage collected.

```javascript
const domElements = new WeakSet();
const element = document.querySelector('.my-element');
domElements.add(element);

// Later, when the element is removed from the DOM
domElements.has(element); // false (garbage collected)
```

#### 2\. Private Data Storage

`WeakSet` can be used to store private data associated with an object without exposing it. Since the references are weak, the data will be automatically removed when the object is no longer reachable.

```javascript
const privateData = new WeakSet();

class MyClass {
  constructor() {
    privateData.add(this);
  }

  #data = 'I am private data';

  getData() {
    if (privateData.has(this)) {
      return this.#data;
    }
    return undefined;
  }
}
```

To see WeakSets in action, don't waste the opportunity to look at my YouTube video about them.

%[https://youtu.be/m3BKqgeVAa4] 

## In Conclusion

WeakSet may not be the most well-known feature of JavaScript, but it offers unique capabilities that can be invaluable in certain situations. By understanding and embracing WeakSet, you can optimize your code, enhance memory management, and unlock the full potential of this hidden gem in the JavaScript universe.

You can find the source code [here](https://github.com/Puppo/javascript-you-dont-know/tree/03-weaksets)