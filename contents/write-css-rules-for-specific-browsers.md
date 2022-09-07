---
layout: layouts/post.njk
title: Write CSS rules for specific browsers
index: 8
---

There are cases where we want styles to target a particular browser. We can use [CSS feature queries](/css-feature-queries) with a declaration that is only available on the target browser.

For example, Firefox is only browser supporting `-moz-appearance: none`, the following snippet can be used to target Firefox only:

```css
@support (-moz-appearance: none) {
    /* Styles for Firefox only */
}
```

The `not` operator is useful to exclude the target browser:

```css
@support not (-moz-appearance: none) {
    /* Styles for browser except Firefox */
}
```

There is another, less popular _hack_ for targeting Firefox only:

```css
@-moz-document url-prefix() {
    /* Styles for Firefox only */
}
```

## Target Safari

```css
@supports (background: -webkit-named-image(i)) {
    /* Styles for Safari only */
}
```

## Target Chromium

Since only Chromium based and Firefox browsers support the `contain: paint` declaration, we can combine `and` and `not` operators to exclude Firefox from the target browsers:

```css
@support (contain: paint) and (not (-moz-appearance: none)) {
    /* Styles for Chromium only */
}
```

Be aware that targeting given browsers with feature queries is still a hack, because the browsers improve their engines continuously, and these properties can be supported or not in the future.
