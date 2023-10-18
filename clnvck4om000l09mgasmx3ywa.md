---
title: "Unlocking the Power of Proxies: JavaScript's Secret Superheroes"
datePublished: Wed Oct 18 2023 06:03:05 GMT+0000 (Coordinated Universal Time)
cuid: clnvck4om000l09mgasmx3ywa
slug: unlocking-the-power-of-proxies-javascripts-secret-superheroes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697438402100/dd6fa71f-5efd-413d-9af4-8f5e18f88c32.png
tags: proxy, js, javascript

---

JavaScript's Proxy object is a powerful feature that enables you to intercept and customize operations performed on objects. This versatile tool allows developers to create more efficient and flexible code while also improving code maintainability. In this article, we will dive into the world of JavaScript proxies, explore their use cases, and provide examples for expert developers.

## A Brief Introduction to Proxies in JavaScript

A Proxy object in JavaScript is used to define custom behaviour for fundamental operations such as property lookup, assignment, enumeration, and function invocation. It acts as a wrapper around another object, called the target, and allows you to intercept and manipulate operations performed on the target object.

### Creating a JavaScript Proxy

To create a JavaScript Proxy, you need two things: a target object and a handler object. The target object is the object you want to wrap with the Proxy, while the handler object defines the custom behaviour for the proxy.

Here's a simple example of creating a Proxy:

```javascript
const target = { name: "John", surname: "Doe", fullName: "John Doe" };
const handler = {
  get(_target, prop) {
    return _target[prop] ? _target[prop].toUpperCase() : "Property not found";
  },
  set(_target, prop, value) {
    if (prop === 'name') {
      _target.fullName = value + ' ' + _target.surname;
    }
    if (prop === 'surname') {
      _target.fullName = _target.name + ' ' + value;
    }
    if (prop === 'fullName') {
      throw new Error('fullName is not writable')
    }
    _target[prop] = value;
    return true;
  }
};

const proxy = new Proxy(target, handler);
console.log(proxy.fullName); // Output: "JOHN DOE"
console.log(proxy.nonexistent); // Output: "Property not found"
proxy.name = 'Jane';
console.log(proxy.fullName); // Output: "Jane Doe"
proxy.surname = 'Smith';
console.log(proxy.fullName); // Output: "Jane Smith"
proxy.fullName = 'Tom Smith'; // Error: fullName is not writable
```

In this example, we defined a `get` trap in the handler object, which intercepts the property lookup operation on the target object. When a property is accessed on the proxy object, the `get` trap is invoked, and it returns the property value in uppercase if the property exists or a custom message if it doesn't.  
Then, we defined a `set` trap, which intercepts a property's set. If the property name is `name` or `surname` calculates the `fullName` and sets the target object with the right value, but if you try to set the `fullName` property the code raises an error.

### Use Cases for Proxies in JavaScript

#### Validation and Constraints

Proxies can be used to enforce data validation and constraints when setting properties on an object. For example, you can ensure that a property value is a certain type or within a specific range.

```javascript
const target = { age: 25 };
const handler = {
  set(_target, prop, value) {
    if (prop === "age" && (typeof value !== "number" || value < 0 || value > 150)) {
      throw new TypeError("Invalid age value");
    }
    _target[prop] = value;
    return true;
  },
};

const proxy = new Proxy(target, handler);
proxy.age = 30; // Works fine
proxy.age = "thirty"; // Throws TypeError: "Invalid age value"
```

#### Logging and Profiling

Proxies can be used to log and profile operations performed on an object, which can be helpful during debugging and performance analysis.

```javascript
const target = { message: "Hello, World!" };
const handler = {
  get(_target, prop) {
    console.log(`Accessing property "${prop}"`);
    return _target[prop];
  },
  set(_target, prop, value) {
    console.log(`Setting property "${prop}" to "${value}"`);
    _target[prop] = value;
    return true;
  },
};

const proxy = new Proxy(target, handler);
console.log(proxy.message); // Logs: "Accessing property "message"" and outputs: "Hello, World!"
proxy.message = "Goodbye, World!"; // Logs: "Setting property "message" to "Goodbye, World!""
```

To learn more don't miss my YouTube video about JavaScript Proxy on my [YouTube channel](https://www.youtube.com/@Puppo_92)

%[https://www.youtube.com/watch?v=e7_lxSrP_Ok] 

## Conclusion

JavaScript's Proxy object is a powerful and versatile feature that allows developers to create more efficient and flexible code. By understanding and utilizing proxies, you can unlock their full potential and become a true JavaScript superhero.

*You can find the code of this article* [*here*](https://github.com/Puppo/javascript-you-dont-know/tree/05-proxies)*.*