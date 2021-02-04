# The enhanced `:not()` pseudo-class enables new kinds of powerful selectors

After a years-long wait, the enhanced `:not()` pseudo-class has finally shipped in Chrome and Firefox, and is now supported in [all major browser engines](https://caniuse.com/css-not-sel-list). This new version of `:not()` accepts [complex selectors](https://drafts.csswg.org/selectors/#complex) and even entire selector lists.

For example, you can now select all `<p>` elements that are _not_ contained within an `<article>` element.

```css
/* select all <p>s that are descendants of <article> */
article p {
}

/* NEW! */
/* select all <p>s that are not descendants of <article> */
p:not(article *) {
}
```

In another example, you may want to select the first list item that does _not_ have the `hidden` attribute (or any other attribute, for that matter). The best selector for this task would be `:nth-child(1 of :not([hidden]))`, but the `of` notation is still [only supported in Safari](https://twitter.com/bramus/status/1343854478005575681). Luckily, this unsupported selector can now be re-written using only the enhanced `:not()` pseudo-class.

```css
/* select all non-hidden elements that are not preceded by a
   non-hidden sibling (i.e., select the first non-hidden child) */
:not([hidden]):not(:not([hidden]) ~ :not([hidden])) {
}
```

https://codepen.io/simevidas/pen/NWbGKNZ?editors=1100

# The HTTP `Refresh` header can be an accessibility issue

The HTTP `Refresh` header (and equivalent HTML `<meta>` tag) is a [very old](https://en.wikipedia.org/wiki/Meta_refresh#History) and [widely supported](https://caniuse.com/mdn-html_elements_meta_http-equiv_refresh) non-standard feature that instructs the browser to automatically and periodically reload the page after a given amount of time.

<!-- prettier-ignore -->
```html
<!-- refresh page after 60 seconds -->
<meta http-equiv="refresh" content="60">
```

According to Google’s data, the `<meta http-equiv="refresh">` tag is used by a whopping [2.8% of page loads](https://www.chromestatus.com/metrics/feature/timeline/popularity/1548) in Chrome (down from 4% a year ago). All these websites risk [failing several success criteria](https://w3c.github.io/wcag/techniques/failures/F41) of the Web Content Accessibility Guidelines (WCAG):

> If the time interval is too short, and there is no way to turn auto-refresh off, people who are blind will not have enough time to make their screen readers read the page before <mark>the page refreshes unexpectedly</mark> and causes the screen reader to begin reading at the top.

However, WCAG does allow using the `<meta http-equiv="refresh">` tag specifically with the value `0` to perform a [client-side redirect](https://w3c.github.io/wcag/techniques/html/H76) in the case that the author does not control the server and hence cannot perform a proper HTTP redirect.

<!-- prettier-ignore -->
```html
<!-- a client-side redirect to another web page -->
<meta http-equiv="refresh" content="0;url='https://example.com'">
```

([via Stefan Judis](https://www.stefanjudis.com/today-i-learned/how-to-refresh-a-page-in-an-interval-without-javascript/))

# How to disable smooth scrolling for the “Find on page…” feature in Chrome

CSS `scroll-behavior: smooth` is [supported](https://caniuse.com/css-scroll-behavior) in Chrome and Firefox. When this declaration is set on the `<html>` element, the browser scrolls the page “[in a smooth fashion](https://drafts.csswg.org/cssom-view/#smooth-scrolling).” This applies to navigations, the standard scrolling APIs (e.g., `window.scrollTo({ top: 0 })`), and scroll snapping operations ([CSS Scroll Snap](https://css-tricks.com/practical-css-scroll-snapping/)).

Unfortunately, Chrome [erroneously](https://bugs.chromium.org/p/chromium/issues/detail?id=866694) keeps smooth scrolling enabled even when the user performs a text search on the page (“Find on page…” feature). Some people find this [annoying](https://twitter.com/chriscoyier/status/1346513455516426242). Until the bug in Chrome is fixed, you can use Christian Schaefer’s clever [CSS workaround](https://schepp.dev/posts/smooth-scrolling-and-page-search/) that effectively disables smooth scrolling for the “Find on page…” feature only.

```css
@keyframes smoothscroll1 {
  from,
  to {
    scroll-behavior: smooth;
  }
}

@keyframes smoothscroll2 {
  from,
  to {
    scroll-behavior: smooth;
  }
}

html {
  animation: smoothscroll1 1s;
}

html:focus-within {
  animation-name: smoothscroll2;
  scroll-behavior: smooth;
}
```

In the following demo, notice how clicking the links scrolls the page smoothly while searching for the words “top” and “bottom” scrolls the page instantly.

https://codepen.io/Schepp/full/wvzNLJz

# Safari still supports the `media` attribute on video sources

With the HTML `<video>` element, it is possible to declare multiple video sources of different MIME types and encodings. This allows websites to use more modern and efficient video formats in supporting browsers, while providing a fallback for other browsers.

<!-- prettier-ignore -->
```html
<video>
  <source src="/flower.webm" type="video/webm">
  <source src="/flower.mp4" type="video/mp4">
</video>
```

In the past, browsers also supported the `media` attribute on video sources. For example, a web page could load a higher-resolution video if the user’s viewport exceeded a certain size.

<!-- prettier-ignore -->
```html
<video>
  <source media="(min-width: 1200px)" src="/large.mp4" type="video/mp4">
  <source src="/small.mp4" type="video/mp4">
</video>
```

The above syntax is in fact still [supported in Safari](https://output.jsbin.com/heniqex/quiet) today, but it was removed from other browsers [around 2014](https://groups.google.com/a/chromium.org/g/blink-dev/c/5sWUMC_d8Tg/m/ZZ0Z7rfeCqUJ) because it was [not considered a good feature](https://lists.w3.org/Archives/Public/public-whatwg-archive/2012May/0171.html):

> It is not appropriate for choosing between low resolution and high resolution because the environment can change (e.g., the user might fullscreen the video after it has begun loading and want high resolution). Also, bandwidth is not available in media queries, but even if it was, <mark>the user agent is in a better position to determine what is appropriate</mark> than the author.

Scott Jehl (Filament Group) [argues](https://twitter.com/scottjehl/status/1349710278481637377) that the removal of this feature was a mistake and that websites should be able to deliver responsive video sources using `<video>` alone.

> For every video we embed in HTML, we’re stuck with the choice of serving source files that are potentially too large or small for many users’ devices … or resorting to more complicated server-side or scripted or third-party solutions to deliver a correct size.

Scott has written a [proposal](https://github.com/filamentgroup/html-video-responsive) for the reintroduction of `media` in video `<source>` elements and is welcoming feedback.

# The CSS `clip-path: path()` function ships in Chrome

It wasn’t mentioned in the latest [“New in Chrome 88” article](https://developer.chrome.com/blog/new-in-chrome-88/), but Chrome just [shipped](https://groups.google.com/a/chromium.org/g/blink-dev/c/E0bpVCaWPEg/m/anYk3vFfAwAJ) the `path()` function for the CSS `clip-path` property, which means that this feature is now supported in all three major browser engines (Safari, Firefox, and Chrome).

The `path()` function is defined in the [CSS Shapes](https://drafts.csswg.org/css-shapes-1/#funcdef-path) module, and it accepts an [SVG path string](https://www.w3.org/TR/SVG11/paths.html#PathData). Chris calls this the [ultimate syntax](https://css-tricks.com/an-initial-implementation-of-clip-path-path/) for the `clip-path` property because it can clip an element with “literally any shape.” For example, here’s a photo clipped with a heart shape:

https://codepen.io/chriscoyier/pen/BObqoy?editors=0100
