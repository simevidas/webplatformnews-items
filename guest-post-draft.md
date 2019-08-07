# Weekly news: CSS `font-style: oblique`, `webhint` browser extension, CSS Modules V1

## Use `font-style: oblique` on variable fonts

Some popular variable fonts have a `'wght'` (weight) axis for displaying text at different font weights and a `'slnt'` (slant) axis for displaying slanted text. This enables creating many font styles using a single variable font file (e.g., see the “[Variable Web Typography](https://zeichenschatz.net/demos/vf/variable-web-typo/)” demo page).

You can use `font-style: oblique` instead of the lower-level `font-variation-settings` property to display slanted text in variable fonts that have a `'slnt'` axis. This approach works in Chrome, Safari, and Firefox.

```css
/* BEFORE */
h2 {
  font-variation-settings: "wght" 500, "slnt" 4;
}

/* AFTER */
h2 {
  font-weight: 500;
  font-style: oblique 4deg;
}
```

https://codepen.io/simevidas/pen/zgRWzz?editors=0100

## The new `webhint` browser extension

The `webhint` linting tool is now available as a browser devtools extension for Chrome, Edge, and Firefox (read [Microsoft’s announcement](https://medium.com/webhint/announcing-the-webhint-browser-extension-abb22f4cfeb)). Compared to Lighthouse, one distinguishing feature of `webhint` are its cross-browser compatibility hints.

![](/media/webhint-extension.png)

## Other news

- **CSS Modules V1** is a new proposal from Microsoft that would extend the JavaScript modules infrastructure to allow importing a `CSSStyleSheet` object from a CSS file (e.g., `import styles from "styles.css";`) — **[source](https://mobile.twitter.com/tomayac/status/1157427266458193922)**

- Web apps installed in the desktop version of Chrome can be uninstalled on the **_about:apps_ page** (right-click on an app’s icon to reveal the _Remove…_ option) — **[source](https://techdows.com/2019/08/how-to-uninstall-pwas-from-chrome-and-microsoft-edge-browsers.html)**

- Because of AMP’s unique requirements, larger news sites such as The Guardian should optimally have **two separate codebases** (one for the AMP pages and one for the regular website) — **[source](https://www.theguardian.com/info/2019/jul/29/revisiting-the-rendering-tier-part-2-migrating-amp)**

Read more news in my new, weekly **Sunday issue**. Visit [webplatform.news](https://webplatform.news) for more information.
