---
layout: layouts/post.njk
tags: post
title: CSS feature queries
index: 5
---

Modern browsers provide a convenient way to detect if a CSS property is supported. The syntax is similar to the media query which starts with `@`:

```css
@support (property: value) {
    /* CSS declarations */
}
```

We can replace the fallback properties used in the [previous technique](/css-fallback-properties):

```css
.list {
    display: flex;
    display: grid;
}
```

with CSS feature queries:

```css
.list {
    display: flex;
}

/* In general speaking, use grid if it is supported by the browser */
@support (display: grid) {
    .list {
        display: grid;
    }
}
```

It's good to know that we can use the `and`, `or` and `not` operators to build a complex query:

```css
@support (...) and (...) {
    /* CSS declarations */
}
@support (...) or (...) {
    /* CSS declarations */
}
```

## Don't use the not operator

The `not` operator tells the browser to apply styles declared inside the `@support` block if it doesn't not support the input declaration.
Let's revise the example above with the opposite approach:

```css
.list {
    display: grid;
}

@supports not (display: grid) {
    .list {
        display: flex;
    }
}
```

By default, the CSS grid is used for the `list` class. It will fallback to the CSS flexbox if the browser doesn't support CSS grid. It seems to be good and works in modern browsers.

What could happen if the browser doesn't understand both CSS grid syntax and `@supports`? IE 11 is one of such browsers. In that scenario, all of our styles aren't effective.
It's recommended to avoid using the `not` operator of CSS feature queries.

## Check for feature queries programmatically

In addition to the declarative way of using `@support`, it's possible to check if a particular CSS declaration is supported programmatically:

```js
if (!CSS || !CSS.supports('display', 'grid')) {
    /* CSS grid isn't supported */
}
```
