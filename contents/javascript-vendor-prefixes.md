---
layout: layouts/post.njk
title: JavaScript vendor prefixes
index: 10
---

With the same reason of [prefixing CSS](/css-vendor-prefixes) properties, the browsers also prefix JavaScript APIs in the experimental phase.
The following table lists out prefixes of most popular browsers:

| Prefix   | Browser(s)                                                                      |
| -------- | ------------------------------------------------------------------------------- |
| `moz`    | Firefox                                                                         |
| `ms`     | Internet Explorer and Microsoft Edge before it uses the Chromium engine         |
| `o`      | The old versions of Opera before it uses the WebKit engine                      |
| `webkit` | Google Chrome, Safari, newer versions of Opera and Edge and almost iOS browsers |

For example, we often used this code to determine if the `requestAnimationFrame` function exists historically:

```js
window.requestAnimationFrame =
    window.requestAnimationFrame ||
    window.mozRequestAnimationFrame ||
    window.webkitRequestAnimationFrame ||
    window.oRequestAnimationFrame ||
    window.msRequestAnimationFrame;
```

If you want to see a more complex scenario, then the full screen APIs might be a perfect example.
Supporting full screen mode must cover the following functionalities:

| Standard API        | Description                                          |
| ------------------- | ---------------------------------------------------- |
| `fullscreenEnabled` | Check if the full screen mode is enabled             |
| `requestFullscreen` | Request browsers to enter the full screen mode       |
| `fullscreenElement` | Return the full screen element                       |
| `fullscreenchange`  | The event triggers when the full screen mode happens |
| `exitFullscreen`    | Exit the full screen mode                            |

We would like to have a wrapper supporting that interface:

```ts
enum Api {
    ExitFullScreen,
    FullScreenChange,
    FullScreenElement,
    FullScreenEnabled,
    RequestFullScreen,
}

type ApiMap = {
    [key in keyof typeof Api]: string;
};
```

Each browser provides a prefixed versions for each API:

```ts
const defaultVendor: ApiMap = {
    ExitFullScreen: 'exitFullscreen',
    FullScreenChange: 'fullscreenchange',
    FullScreenElement: 'fullscreenElement',
    FullScreenEnabled: 'fullscreenEnabled',
    RequestFullScreen: 'requestFullscreen',
};

const webkitVendor: ApiMap = {
    ExitFullScreen: 'webkitExitFullscreen',
    FullScreenChange: 'webkitfullscreenchange',
    FullScreenElement: 'webkitFullscreenElement',
    FullScreenEnabled: 'webkitFullscreenEnabled',
    RequestFullScreen: 'webkitRequestFullscreen',
};

const mozVendor: ApiMap = {
    ExitFullScreen: 'mozCancelFullScreen',
    FullScreenChange: 'mozfullscreenchange',
    FullScreenElement: 'mozFullScreenElement',
    FullScreenEnabled: 'mozFullScreenEnabled',
    RequestFullScreen: 'mozRequestFullScreen',
};

const msVendor: ApiMap = {
    ExitFullScreen: 'msExitFullscreen',
    FullScreenChange: 'msFullscreenChange',
    FullScreenElement: 'msFullscreenElement',
    FullScreenEnabled: 'msFullscreenEnabled',
    RequestFullScreen: 'msRequestFullscreen',
};
```

Finally, we can get the APIs set supported by the current browser:

```ts
const vendor: ApiMap =
    (Api.FullScreenEnabled in document && defaultVendor) ||
    (webkitVendor.FullScreenEnabled in document && webkitVendor) ||
    (msVendor.FullScreenEnabled in document && msVendor) ||
    defaultVendor;
```

Requesting the full screen mode for a given element can be invoked simply:

```js
element[vendor.RequestFullScreen]();
```

## See also

-   [CSS vendor prefixes](/css-vendor-prefixes)
