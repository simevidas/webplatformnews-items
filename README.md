# Now may be a good time to start using `:focus-visible`

The CSS `:focus-visible` pseudo-class replaces `:focus` as the new way to create custom focus indicators for keyboard users. Chrome itself recently switched from `:focus` to `:focus-visible` in the user agent stylesheet, and as a result of that change, the default focus ring is [no longer shown](https://css-tricks.com/weekly-platform-news-focus-rings-donut-scope-ditching-em-units-and-global-privacy-control/#chrome-will-stop-displaying-focus-rings-when-clicking-buttons) when the user clicks or taps a button.

When switching from `:focus` to `:focus-visible`, consider backwards compatibility. Your keyboard focus indicators should be clearly visible in all browsers, not just the ones that [support `:focus-visible`](https://caniuse.com/css-focus-visible). If you only style `:focus-visible`, non-supporting browsers will show the default focus ring, which depending on your design “[may not be sufficiently clear or visible at all](https://www.tpgi.com/focus-visible-and-backwards-compatibility/#comment-1184).”

```css
button {
  background: white;
}

button:focus-visible {
  outline: none;
  background: #ffdd00; /* gold */
}
```

![](/media/safari-focus-ring-invisible.png)

A good way to start using `:focus-visible` today is to define the focus styles in a `:focus` rule and then immediately undo these same styles in a `:focus:not(:focus-visible)` rule. This is admittedly not the most elegant and intuitive pattern, but it works well in all browsers:

- Browsers that don’t support `:focus-visible` use the focus styles defined in the `:focus` rule and ignore the second style rule completely (because `:focus-visible` is unknown to them).
- In browsers that do support `:focus-visible`, the second style rule reverts the focus styles defined in the `:focus` rule if the `:focus-visible` state isn’t active as well. In other words, the focus styles defined in the `:focus` rule are only in effect when `:focus-visible` is also active.

```css
button:focus {
  outline: none;
  background: #ffdd00; /* gold */
}

button:focus:not(:focus-visible) {
  background: white; /* undo gold */
}
```

# The BBC created a more accessible typeface

The BBC [created](https://abilitynet.org.uk/news-blogs/accessible-typeface-designed-bbc) their own custom typeface called Reith (named after the BBC’s founder Sir John Reith). Their goal was to create a font that supports multiple languages and is easier to read, especially on small devices. The font was tested with mixed-ability user groups (dyslexia and vision impairment) and across different screen sizes.

> We [the BBC] were using Helvetica or Arial. We also had Gill Sans as the corporate typeface. These typefaces were designed a hundred years ago for the printed page [and] don’t perform well on today’s modern digital screens.

<figure>
    <img src="/media/bbc-sport-reith-sans.jpg" alt="">
    <figcaption>Reith Sans can bee seen in use on <a href="https://www.bbc.com/sport">BBC Sport</a></figcaption>
</figure>

**Note:** If you’d like to inspect Reith Sans and Reith Serif in [Wakamai Fondue](https://wakamaifondue.com/beta/), you can quickly access the URLs of the WOFF2 files in the “All fonts on page” section of the Fonts pane in Firefox’s DOM inspector on BBC’s website.

# `display: contents` is still not accessible in Safari

The CSS `display: contents` value is supported in browsers [since 2018](https://css-tricks.com/get-ready-for-display-contents/). An element with this value “[does not generate any boxes](https://drafts.csswg.org/css-display/#box-generation)” and is effectively replaced by its children. This is especially useful in flex and grid layouts, where the `contents` value can be used to “promote” more deeply nested elements to flex/grid items while retaining a semantic document structure.

<figure>
    <img src="/media/css-display-contents-semantic-structure.png" alt="">
    <figcaption>Source: <a href="https://blogs.igalia.com/mrego/2018/01/11/display-contents-is-coming/">Manuel Rego Casasnovas</a></figcaption>
</figure>

Unfortunately, this feature originally shipped with an [implementation bug](https://github.com/w3c/csswg-drafts/issues/3040) that removed the element from the browser’s accessibility tree. For example, applying `display: contents` to a `<ul>` element had as a consequence that the element was no longer mentioned by screen readers. Since then, this bug has been fixed in Firefox and Chrome ([in the latest version](https://rachelandrew.co.uk/archives/2021/03/11/good-news-about-display-contents-and-chrome/)).

INSERT VIDEO - /media/css-display-contents-screen-reader.mp4

VIDEO CAPTION: ([code on CodePen](https://codepen.io/simevidas/pen/MWJGRaJ?editors=1100))

In Chrome and Firefox, the screen reader informs the user that the “Main, navigation” contains a “list, 2 items.” In Safari, the latter part is missing because the `<ul>` and `<li>` elements are not present in the accessibility tree. Until Apple fixes this [bug in Safari](https://bugs.webkit.org/show_bug.cgi?id=185679), be careful when using the `contents` value on semantic elements and test in screen readers to confirm that your pages are accessible in Safari as well.

# Set `opacity` when overriding the color of placeholder text

Accessibility experts recommend [avoiding placeholders](https://www.deque.com/blog/accessible-forms-the-problem-with-placeholders/) if possible because they can be confused for pre-populated text and disappear when the user starts entering a value. However, many websites (including Wikipedia and GOV.UK) use placeholders in simple web forms that contain only a single input field, such as a search field.

<figure>
    <img src="/media/css-tricks-newsletter-form.png" alt="">
    <figcaption>The subscription form for the CSS-Tricks newsletter uses a placeholder in the email field</figcaption>
</figure>

Placeholders can be styled via the widely supported `::placeholder` pseudo-element. If your design calls for a custom color for placeholder text, make sure to specify both `color` and `opacity`. The latter is needed for Firefox, which [applies](https://searchfox.org/mozilla-central/source/layout/style/res/forms.css#213-215) `opacity: 0.54` to `::placeholder` by default. If you don’t override this value, your placeholder text may have insufficient contrast in Firefox.

```css
.search-field::placeholder {
  color: #727272;
  opacity: 1; /* needed for Firefox */
}
```

<figure>
    <img src="/media/ebay-placeholder-contrast-issue.png" alt="">
    <figcaption>The placeholder text on eBay’s website is lighter in Firefox and doesn’t meet the <a href="https://w3c.github.io/wcag/guidelines/#contrast-minimum">minimum contrast requirement</a> of 4.5:1</figcaption>
</figure>

# Declarative Shadow DOM could help popularize style encapsulation

One of the key features of Shadow DOM is style encapsulation, wherein the outer page’s style rules don’t match elements inside the shadow tree, and vice versa. In order to use this feature, you need to attach a shadow DOM tree to an element (usually, a custom element like `<my-element>`) and copy the element’s template (usually, from a `<template>` element in the DOM) to the element’s newly created shadow DOM.

These steps can only be performed in JavaScript. If you’re only interested in style encapsulation and don’t need any dynamic functionality for your element, here is the [minimum amount of JavaScript](https://twitter.com/MiriSuzanne/status/1369347329652756481) required to create a custom element with a shadow DOM:

```js
customElements.define(
  "my-element",
  class extends HTMLElement {
    constructor() {
      super();

      // find <template id="my-template"> in the DOM
      let template = document.getElementById("my-template");

      // make a copy of the template contents…
      let content = template.content.cloneNode(true);

      // …and inject it into <my-element>’s shadow DOM
      this.attachShadow({ mode: "open" }).appendChild(content);
    }
  }
);
```

For an example of style encapsulation, see Miriam Suzanne’s `<media-object>` element [on CodePen](https://codepen.io/mirisuzanne/pen/GRNwmpm). The scoped styles are located in the `<template>` element in the HTML pane. Notice how this CSS code can use simple selectors, such as `article`, that only match elements inside `<media-object>`’s shadow DOM.

JavaScript may soon no longer be required to create this type of style encapsulation in modern browsers. Earlier this week, Chrome became the first browser to ship Google’s [Declarative Shadow DOM](https://developer.chrome.com/en/blog/new-in-chrome-90/#declarative) proposal. If it becomes a standard, this feature will also make it possible to use Shadow DOM in combination with server-side rendering.
