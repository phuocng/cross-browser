---
layout: layouts/post.njk
title: CSS fallback properties
index: 1
---

A CSS class can consist of many declarations whose each of them has the syntax of `property: value` syntax:

```css
.cls {
    property: value;
}
```

We can set different values for the same property. The browser will try to use the last declaration. In the case it can't recognize the declaration, it will fallback to the previous value until the supported value is found.

It is the right place to add prefixes for browser vendors here. Remember in the old days, we often use this technique to set a linear gradient for the header element:

```css
.header {
    background-image: url(/path/to/fallback-gradient.svg);
    background-image: -webkit-gradient(...);
    background-image: -webkit-linear-gradient(...);
    background-image: -moz-linear-gradient(...);
    background-image: -ms-linear-gradient(...);
    background-image: -o-linear-gradient(...);
    background-image: linear-gradient(...);
}
```

Even though the specific `linear-gradient()` function is supported in modern browsers, the technique is still useful in many cases. The following sample code reverts to CSS flexbox if CSS grid isn't supported:

```css
.list {
    display: flex;
    display: grid;
}
```
