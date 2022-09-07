---
layout: layouts/post.njk
title: Create a JavaScript polyfill
index: 9
---

Due to the fact that JavaScript APIs have their own specifications, not all the browsers support a particular specification at the same time. A JavaScript API can be implemented in a browser sooner or later than the other browsers.

Because of that, we have to provide a patch version of the API to make sure that it still works on browsers that don't support it natively. That kind of patch is called polyfill.

The sample code below provides a patch for the Array's `at()` method which isn't available on Safari earlier than 15.4:

```js
if (!Array.prototype.at) {
    Array.prototype.at = function (index) {
        // The implementation ...
    };
}
```

We can get rid of the `if` statement:

```js
Array.prototype.at =
    Array.prototype.at ||
    function (index) {
        // The implementation ...
    };
```

It's also possible to polyfill a global function using a similar approach. The `structedClone` function which isn't available on Safari earlier than 15.4, can be polyfilled as following:

```js
if (typeof window.structuredClone !== 'function') {
    window.structuredClone = function (value) {
        // ...
    };
}

// Or
typeof window.structuredClone !== 'function' &&
    window.structuredClone = function (value) {
        // ...
    };
```
