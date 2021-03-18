# The `prefers-contrast: more` media query is supported in Safari Preview

After `prefers-reduced-motion` in 2017, `prefers-color-scheme` in 2019, and `forced-colors` in 2020, a fourth [user preference media feature](https://drafts.csswg.org/mediaqueries-5/#mf-user-preferences) is making its way to browsers. The CSS `prefers-contrast: more` media query is now [supported](https://webkit.org/blog/11525/release-notes-for-safari-technology-preview-119/) in the preview version of Safari. This feature will allow websites to honor the users’ preference for increased contrast.

> **_more_**
>
> Indicates that user has notified the system that they prefer an interface that has a higher level of contrast.

<figure>
    <img src="/media/apple-increase-contrast-option.png" alt="">
    <figcaption>Apple could use this new media query to increase the contrast of gray text on its website</figcaption>
</figure>

```css
.pricing-info {
  color: #86868b; /* contrast ratio 3.5:1 */
}

@media (prefers-contrast: more) {
  .pricing-info {
    color: #535283; /* contrast ratio 7:1 */
  }
}
```

# Making math a first-class citizen on the web

One of the earliest specifications developed by the W3C in the mid-to-late ’90s was a markup language for displaying mathematical notations on the web called MathML. This language is currently [supported](https://caniuse.com/mathml) in Firefox and Safari. Chrome’s implementation was removed [in 2013](https://www.cnet.com/news/google-subtracts-mathml-from-chrome-and-anger-multiplies/) because of “concerns involving security, performance, and low usage on the Internet.”

INSERT CODEPEN - https://codepen.io/simevidas/pen/YzpbwRa?editors=1000

**Note:** If you’re using Chrome or Edge, enable “Experimental Web Platform features” on the about:flags page to view the demo.

There is a renewed effort to properly integrate MathML into the web platform and bring it to all browsers in an interoperable way. Igalia has been developing a MathML implementation for Chromium [since 2019](https://mathml.igalia.com/news/2019/02/12/launch-of-the-project/). The new specification [MathML Core Level 1](https://mathml-refresh.github.io/mathml-core/) is a [fundamental subset](https://www.chromestatus.com/feature/5240822173794304) of MathML 3 (2014) that is “[most suited for browser implementation](https://twitter.com/w3cdevs/status/1359892583460311040).” If approved by the W3C, a new [Math Working Group](https://w3c.github.io/charter-drafts/math-2020.html) will work on improving the accessibility and searchability of MathML.

> The mission of the Math Working Group is to promote the inclusion of mathematics on the Web so that it is a first-class citizen of the web that displays well, is accessible, and is searchable.

# CSS `:is()` upgrades selector lists to become forgiving

The new CSS [`:is()`](https://drafts.csswg.org/selectors-4/#matches) and [`:where()`](https://drafts.csswg.org/selectors-4/#zero-matches) pseudo-classes are now supported in Chrome, Safari, and Firefox. In addition to their [standard use-cases](https://css-tricks.com/css-is-and-where-are-coming-to-browsers/) (reducing repetition and keeping specificity low), these pseudo-classes can also be used to make selector lists “[forgiving](https://drafts.csswg.org/selectors-4/#forgiving-selector).”

> For legacy reasons, the general behavior of a selector list is that if any selector in the list fails to parse … the entire selector list becomes invalid. This can make it hard to write CSS that uses new selectors and still works correctly in older user agents.

In [other words](https://css-tricks.com/one-invalid-pseudo-selector-equals-an-entire-ignored-selector/), “if any part of a selector is invalid, it invalidates the whole selector.” However, wrapping the selector list in `:is()` makes it forgiving: Unsupported selectors are simply ignored, but the remaining selectors will still match.

Unfortunately, pseudo-elements do not work inside `:is()` (although that may [change in the future](https://github.com/w3c/csswg-drafts/issues/2284#issuecomment-541909879)), so it is currently not possible to turn two vendor-prefixed pseudo-elements into a forgiving selector list to [avoid repeating styles](https://twitter.com/JoshWComeau/status/1359213597331763200).

<!--prettier-ignore -->
```css
/* One unsupported selector invalidates the entire list */
::-webkit-slider-runnable-track, ::-moz-range-track {
  background: red;
}

/* Pseudo-elements do not work inside :is() */
:is(::-webkit-slider-runnable-track, ::-moz-range-track) {
  background: red;
}

/* Thus, the styles must unfortunately be repeated */
::-webkit-slider-runnable-track {
  background: red;
}
::-moz-range-track {
  background: red;
}

```

# Dell and Kraft Heinz sued over inaccessible websites

More and more American businesses are facing lawsuits over accessibility issues on their websites. Most recently, the tech corporation Dell was [sued](https://www.theregister.com/2021/03/05/giannaros_v_dell/) by a visually impaired person who was unable to navigate Dell’s website and online store using the JAWS and VoiceOver screen readers.

> The Defendant fails to communicate information about its products and services effectively because <mark>screen reader auxiliary aids cannot access important content</mark> on the Digital Platform. … The Digital Platform uses visual cues to convey content and other information. Unfortunately, screen readers cannot interpret these cues and communicate the information they represent to individuals with visual disabilities.

Earlier this year, Kraft Heinz Foods Company was [sued](https://www.boia.org/blog/kraft-heinz-company-sued-kool-aid-site-alleged-to-not-be-accessible) for failing to comply with the [Web Content Accessibility Guidelines](https://w3c.github.io/wcag/guidelines/) on one of the company’s websites. The complaint alleges that the website did not declare a language (`lang` attribute) and provide accessible labels for its image links, among other things.

In the United States, the Americans with Disabilities Act (ADA) [applies](https://www.latimes.com/politics/story/2019-10-07/blind-person-dominos-ada-supreme-court-disabled) to websites, which means that people can sue retailers if their websites are not accessible. According to the CEO of Deque Systems (the makers of [axe](https://www.deque.com/axe/)), the recent trend of increase in web-based ADA lawsuits can be [attributed](https://www.deque.com/blog/the-state-of-accessibility-gaad-2019/) to a lack of a single overarching regulation that would provide specific compliance requirements.

# `background-clip` and `background-origin` have different initial values

By default, a CSS background is painted within the element’s border box (`background-clip: border-box`) but positioned relative to the element’s padding box (`background-origin: padding-box`). This inconsistency can result in [unexpected patterns](https://twitter.com/AmeliasBrain/status/1360303122543902720) if the element’s border is semi-transparent or dotted/dashed.

<img src="/media/css-background-unexpected-pattern.png" alt="">

```css
.box {
  /* semi-transparent border */
  border: 20px solid rgba(255, 255, 255, 0.25);

  /* background gradient */
  background: conic-gradient(
    from 45deg at bottom left,
    deeppink,
    rebeccapurple
  );
}
```

Because of the different initial values, the background gradient in the above image is repeated as a tiled image on all sides under the semi-transparent border. In this case, positioning the background relative to the border box (`background-origin: border-box`) makes more sense.

INSERT CODEPEN - https://codepen.io/simevidas/full/mdOYYRa
