# Weekly news: Preventing image loads with `<picture>`, The Web We Want, `<svg>` styles are not scoped

## Preventing image loads with `<picture>`

You can use the `<picture>` element to prevent an image from loading if a specific media query matches the user’s environment (e.g., if the viewport width is larger or smaller than a certain length value). [Try out the demo](https://codepen.io/simevidas/pen/voZENR?editors=1000).

```html
<picture>
  <!-- show 1⨯1 transparent image if viewport width ≤ 40em -->
  <source
    media="(max-width: 40em)"
    srcset="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"
  />

  <!-- only load image if viewport width > 40em -->
  <img src="product-large-screen.png" />
</picture>
```

**Source:** [Scott Jehl’s post on Twitter](https://mobile.twitter.com/scottjehl/status/1154424344388558848)

## The Web We Want

The Web We Want ([webwewant.fyi](https://webwewant.fyi/)) is a new collaboration between browser vendors that aims to collect feedback from web developers about the current state of the web. You can submit a feature request on the website (“What do you want?”) and get a chance to present it at an event (An Event Apart, Smashing Conference, etc.).

![](/media/web-we-want.png)

**Source:** [Aaron Gustafson’s announcement on WICG](https://discourse.wicg.io/t/share-your-biggest-challenges-with-the-broader-community/3750?u=simevidas)

## In other news

- Firefox supports a non-standard Boolean parameter for the **`location.reload` method** that can be used to hard-reload the page (bypassing the browser’s HTTP cache) — **[source](https://mobile.twitter.com/wilsonpage/status/1149634930168590336)**

- If you use inline `<svg>` elements that itself have inline CSS code (in `<style>` elements), be aware that those **styles are not scoped** to the SVG element but global, so they affect other SVG elements as well — **[source](https://mobile.twitter.com/SaraSoueidan/status/1153947911526453249)**

- **XSS Auditor**, a Chrome feature that detects cross-site scripting vulnerabilities, has been deemed ineffective and will be removed from Chrome in a future version. You may still want to set the HTTP X-Xss-Protection: 1; mode=block header for legacy browsers — **[source](https://scotthelme.co.uk/security-headers-updates/)**

Read more news in Web Platform News’s **weekly Sunday issue**. Visit [webplatform.news](https://webplatform.news) for more information.
