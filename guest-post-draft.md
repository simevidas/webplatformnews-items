# Weekly news: Improving UX on slow connections, tip for writing alt text, HTML `loading` attribute polyfill

## Detecting users on slow connections

Algolia is using the Network Information API (see the API’s [Chrome status page](https://www.chromestatus.com/feature/5108786398232576)) to detect users on slow connections — about 9% of their users — and make the following adjustments to ensure a good user experience:

- increase the request timeout when the user performs a search query (a static timeout can cause a false positive for users on slow connections)

- show a notification to the user while they’re waiting for search results (e.g., “You are on a slow connection. This might take a while.”)

- request fewer search results to decrease the total response size

- debounce queries (e.g., don’t send queries at every keystroke)

```js
navigator.connection.addEventListener("change", () => {
  // effective round-trip time estimate in ms
  let rtt = navigator.connection.rtt;

  // effective connection type
  let effectiveType = navigator.connection.effectiveType;

  if (rtt > 500 || effectiveType.includes("2g")) {
    // slow connection
  }
});
```

<small>(via [Jonas Badalic](https://blog.algolia.com/netinfo-api-algolia-javascript-client/))</small>

## Alt text should communicate the main point

> The key is to describe what you want your audience to get out of the image rather than a simple description of what the image is.

<!-- prettier-ignore -->
```html
<!-- BEFORE -->
<img alt="Graph showing the use of the phrase “Who you
          gonna call?” in popular media over time.">

<!-- AFTER -->
<img alt="Graph illustrating an 800% increase in the use
          of the phrase “Who you gonna call?” in popular
          media after the release of Ghostbusters on
          June 7th, 1984.">
```

<small>(via [Caitlin Cashin](https://www.deque.com/blog/accessibility-strategies-for-your-content-team/))</small>

## In other news…

- There is a new polyfill for the **HTML `loading` attribute** that is used by wrapping the images and iframes that you want to lazy-load in `<noscript>` elements (via [Maximilian Franzke](https://twitter.com/maedmaex/status/1159473838956175365))

- WeChat, the **Chinese multi-purpose app** with over 1 billion monthly active users, hosts over 1 million “mini programs” that are built in a very similar fashion to web apps (essentially CSS and JavaScript) (via [Thomas Steiner](https://twitter.com/tomayac/status/1161947030530547713))

- Microsoft has made 24 new (online) voices from 21 different languages available to the Speech Synthesis API in the preview version of Edge (“these voices are **the most natural-sounding voices** available today”) (via [Scott Low](https://blogs.windows.com/msedgedev/2019/08/14/cloud-powered-voices-microsoft-edge-chromium/))

Read more news in my new, weekly **Sunday issue**. Visit [webplatform.news](https://webplatform.news) for more information.
