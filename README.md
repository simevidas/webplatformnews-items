# Chrome will stop displaying focus rings when clicking buttons

Chrome, Edge, and other Chromium-based browsers display a focus indicator (a.k.a. focus ring) when the user clicks or taps a ([styled](https://twitter.com/myakura/status/1366972939384487936)) button. For comparison, Safari and Firefox don’t display a focus indicator when a button is clicked or tapped but only when the button is focused via the keyboard.

INSERT VIDEO WITH CAPTION - /media/chrome-button-click-focus-indicator.mp4

<figure>
    <video src="/media/chrome-button-click-focus-indicator.mp4" controls width="864" height="486"></video>
    <figcaption>The focus ring will stay on the button until the user clicks somewhere else on the page</figcaption>
</figure>

Some developers find this behavior [annoying](https://twitter.com/LeaVerou/status/1045768279753666562) and are using various [workarounds](https://twitter.com/adamwathan/status/1244340194280648704) to prevent the focus ring from appearing when a button is clicked or tapped. For example, the popular [what-input library](https://github.com/ten1seven/what-input) continuously tracks the user’s input method (mouse, keyboard or touch), allowing the page to suppress focus rings specifically for mouse clicks.

```css
[data-whatintent="mouse"] :focus {
  outline: none;
}
```

A more recent workaround was enabled by the addition of the CSS `:focus-visible` pseudo-class to Chromium a few months ago. In the current version of Chrome, clicking or tapping a button invokes the button’s `:focus` state but not its `:focus-visible` state, so the page can use a suitable selector to suppress focus rings for clicks and taps without affecting keyboard users.

```css
:focus:not(:focus-visible) {
  outline: none;
}
```

Fortunately, these workarounds will soon become unnecessary. Chromium’s user agent stylesheet recently [switched](https://blogs.igalia.com/mrego/2021/03/01/focus-visible-in-webkit-february-2021/#default-user-agent-style-sheet) from `:focus` to `:focus-visible`, and as a result of this change, button clicks and taps no longer invoke focus rings. The new behavior will first ship in Chrome 90 next month.

# The enhanced CSS `:not()` selector enables “donut scope”

I recently [wrote](https://css-tricks.com/weekly-platform-news-the-not-pseudo-class-video-media-queries-clip-path-path-support/#the-enhanced-not-pseudo-class-enables-new-kinds-of-powerful-selectors) about the `A:not(B *)` selector pattern that allows authors to select all `A` elements that are not descendants of a `B` element. This pattern can be expanded to `A B:not(C *)` to create a “[donut scope](https://twitter.com/LeaVerou/status/1354760561087676416).”

For example, the selector `article p:not(blockquote *)` matches all `<p>` elements that are descendants of an `<article>` element but not descendants of a `<blockquote>` element. In other words, it selects all paragraphs in an article except the ones that are in a block quotation.

<figure>
  <img src="/media/css-not-donut-scope.png" alt="">
  <figcaption>The donut shape that gives this scope its name</figcaption>
</figure>

INSERT CODEPEN - https://codepen.io/simevidas/pen/bGBKZzY?editors=0100

# The New York Times now honors Global Privacy Control

Announced [last October](https://globalprivacycontrol.org/press-release/20201007.html), Global Privacy Control (GPC) is a new privacy signal for the web that is designed to be legally enforceable. Essentially, it’s an HTTP `Sec-GPC: 1` request header that tells websites that the user does not want their personal data to be shared or sold.

<figure>
  <img src="/media/http-sec-gpc-header.png" alt="">
  <figcaption>The DuckDuckGo Privacy Essentials extension enables GPC by default in the browser</figcaption>
</figure>

The New York Times has become the first major publisher to honor GPC. A number of other publishers, including The Washington Post and Automattic (WordPress.com), have committed to honoring it “[this coming quarter](https://globalprivacycontrol.org/press-release/20210128).”

From [NYT’s privacy page](https://www.nytimes.com/privacy):

> **Does The Times support the Global Privacy Control (GPC)?**
>
> Yes. When we detect a GPC signal from a reader’s browser where GDPR, CCPA or a similar privacy law applies, <mark>we stop sharing the reader’s personal data</mark> online with other companies (except with our service providers).

# The case for `em`-based media queries

Some browsers allow the user to **increase the default font size** in the browser’s settings. Unfortunately, this user preference has no effect on websites that set their font sizes in pixels (e.g., `font-size: 20px`). In part for this reason, some websites (incl. CSS-Tricks) instead use [font-relative units](https://drafts.csswg.org/css-values-4/#font-relative-lengths), such as `em` and `rem`, which _do_ respond to the user’s font size preference.

![](/media/css-tricks-font-relative-units.png)

Ideally, a website that uses font-relative units for `font-size` should also use [`em` values in media queries](https://zellwk.com/blog/media-query-units/) (e.g., `min-width: 80em` instead of `min-width: 1280px`). Otherwise, the site’s responsive layout may not always work as expected.

For example, CSS-Tricks switches from a two-column to a one-column layout on narrow viewports to prevent the article’s lines from becoming too short. However, if the user increases the default font size in the browser to `24px`, the text on the page will become larger (as it should) but the page layout will not change, resulting in extremely short lines at certain viewport widths.

INSERT YOUTUBE VIDEO - https://www.youtube.com/watch?v=FrW9vTPGhrM

If you’d like to try out `em`-based media queries on your website, there is a [PostCSS plugin](https://github.com/niksy/postcss-em-media-query) that automatically converts `min-width`, `max-width`, `min-height`, and `max-height` media queries from `px` to `em`.

([via Nick Gard](https://uxdesign.cc/say-goodbye-to-pixels-cb720fbaf250))

# A new push to bring CSS `:user-invalid` to browsers

In 2017 Peter-Paul Koch published a series of [three articles](https://twitter.com/ppk/status/942726306944442369) about native form validation on the web. [Part 1](https://www.quirksmode.org/blog/archives/2017/12/native_form_val.html) points out the problems with the widely supported CSS [`:invalid`](https://developer.mozilla.org/en-US/docs/Web/CSS/:invalid) pseudo-class:

- The validity of `<input>` elements is re-evaluated on every key stroke, so a form field can become `:invalid` while the user is still typing the value.

- If a form field is required (`<input required>`), it will become `:invalid` immediately on page load.

Both of these behaviors are potentially confusing (and [annoying](https://twitter.com/ryanflorence/status/1354502174332444673)), so websites cannot rely solely on the `:invalid` selector to indicate that a value entered by the user is not valid. However, there is the option to [combine](https://www.bram.us/2021/01/28/form-validation-you-want-notfocusinvalid-not-invalid/) `:invalid` with `:not(:focus)` and even `:not(:placeholder-shown)` to ensure that the page’s “invalid” styles do not apply to the `<input>` until the user has finished entering the value and moved focus to another element.

INSERT CODEPEN - https://codepen.io/bramus/pen/ExNYBOK?editors=0100

The CSS Selectors module defines a [`:user-invalid`](https://drafts.csswg.org/selectors/#user-pseudos) pseudo-class that avoids the problems of `:invalid` by only matching an `<input>` “after the user has significantly interacted with it.”

![](/media/css-user-invalid-example.png)

Firefox already supports this functionality via the `:-moz-ui-invalid` pseudo-class (see it in action [here](https://twitter.com/simevidas/status/1366281785122955264)). Mozilla now [intends](https://groups.google.com/g/mozilla.dev.platform/c/rEYMl79krS8/m/UI_kwzatCAAJ) to un-prefix this pseudo-class and ship it under the standard `:user-invalid` name. There are still no signals from other browser vendors, but the Chromium and WebKit bugs for this feature have been filed.
