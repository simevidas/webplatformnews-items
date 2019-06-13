# Weekly news: CSS Scroll Snap, Opera GX, PWA install icon

`<EDITOR_INTRO>`  
Šime posts regular content for web developers on [webplatform.news](https://webplatform.news).  
`</EDITOR_INTRO>`

## An install icon is coming to Chrome on desktop

[Pete LePage](https://developers.google.com/web/updates/2019/06/pwa-install-addressbar): The next version of Chrome will automatically show an install icon in the address bar on desktop if the site meets Chrome’s PWA installability criteria. (You can listen for the `appinstalled` event to detect if the user installed your PWA.)

![](/media/chrome-pwa-install-icon.png)

## Opera GX is available on Windows

[Maciej Kocemba](https://blogs.opera.com/desktop/2019/06/opera-gx-early-access-lvl1/): The preview version of Opera GX for Windows is now available. This is a special version of Opera that lets users limit how much CPU and RAM is available to the browser.

![](/media/opera-gx-cpu-ram-limiter.png)

## Updated ECMAScript proposals

[Azu](https://ecmascript-daily.github.io/ecmascript/2019/06/09/ecmascript-proposal-updates): The JavaScript optional chaining operator (`obj?.prop`) and nullish coalescing operator (`x ?? y`) proposals have been moved to Stage 2 of the TC39 process. (Ed. note: See [Web Platform News issue 902](https://webplatform.news/issues/2017-05-26) for more information about the TC39 process.)

```js
// BEFORE
let text = response.settings && response.settings.headerText;
if (text == null) text = "Hello, world!";

// AFTER
let text = response.settings?.headerText ?? "Hello, world!";
```

## CSS Scroll Snap is coming to Firefox

[Šime Vidas](https://webplatform.news/issues/2019-06-05): CSS Scroll Snap is supported in Chrome, Safari, and the next version of Firefox. Scroll snapping works well on touch screen devices but there are some usability issues on desktop platforms.

<video controls src="/media/css-scroll-snap-demo.mp4">
