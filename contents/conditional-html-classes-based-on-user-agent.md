---
layout: layouts/post.njk
title: Conditional HTML classes based on user agent
index: 3
---

In the [previous post](/conditional-html-classes), we use the conditional comment tags to add specific CSS classes to the root `html` element:

```html
<!--[if lt IE 7]><html class="lt-ie7 lt-ie8 lt-ie9"><![endif]-->
<!--[if IE 7]><html class="lt-ie8 lt-ie9"><![endif]-->
<!--[if IE 8]><html class="lt-ie9"><![endif]-->
```

The conditional comments are ignored on other browsers except Internet Explorer (IE). The tag is also disabled from IE 10. How can we add additional classes for other browsers and older versions of IE?

We can detect a browser and its version based on the user agent. The following snippet checks if the current browser is IE 11 and adds corresponding CSS class if needed:

```js
function detectIE11() {
    if (navigator.userAgent.match(/Trident.*rv:11\./)) {
        document.documentElement.classList.add('ie11');
    }
}
```

As soon as the `ie11` class added to the root `html` element, you can add more styles explicitly for IE 11:

```css
.ie11 .otherClass {
    /* Styles for IE 11 */
}
```

The approach not only works with IE 11, but also can be used to support other browsers.
