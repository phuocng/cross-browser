---
layout: layouts/post.njk
tags: post
title: CSS vendor prefixes
index: 6
---

Before a CSS property or JavaScript API is standardized and becomes popular, each browser tries to support it differently by its own engine. We can give it a try by using a different syntax.

A property might need to be prefixed with an identifier indicating the corresponding browsers, for example:

| Prefix     | Browser(s)                                                              |
| ---------- | ----------------------------------------------------------------------- |
| `-moz-`    | Firefox                                                                 |
| `-ms-`     | Internet Explorer and Microsoft Edge before it uses the Chromium engine |
| `-o-`      | The old versions of Opera before it uses the WebKit engine              |
| `-webkit-` | Google Chrome, Safari and newer versions of Opera and Edge              |

Let's take a look at a simple example. In the old days when the `transition` property is not standardized, we usually had to prefix it to make sure it works in popular browsers:

```css
-webkit-transition: all 400ms ease;
-moz-transition: all 400ms ease;
-ms-transition: all 400ms ease;
-o-transition: all 400ms ease;
transition: all 400ms ease;
```

However, the `transtion` property is a standard property currently and supported by all modern browsers, we just simply remove all prefixes:

```css
transition: all 400ms ease;
```

Do we need to track properties which have been standardized and work without being prefixed?

Fortunately, there are more tools to automate the process. They prefix a CSS property automatically based on the data covering which browsers (including versions) support that property.
[Autoprefixer](https://github.com/postcss/autoprefixer) is one of the most popular tools.
