# Logical CSS could soon become the new default

Six years after Mozilla shipped the [first bits](https://lists.w3.org/Archives/Public/www-style/2015Jul/0040.html) of [CSS Logical Properties](https://drafts.csswg.org/css-logical-1/) in Firefox, this feature is now on a path to full browser support in 2021. The categories of logical properties and values listed in the table below are already supported in Firefox, Chrome, and the latest Safari Preview.

| CSS property or value | The logical equivalent |
| :-------------------: | :--------------------: |
|     `margin-top`      |  `margin-block-start`  |
|  `text-align: right`  |   `text-align: end`    |
|       `bottom`        |   `inset-block-end`    |
|     `border-left`     | `border-inline-start`  |
|         (n/a)         |    `margin-inline`     |

Logical CSS also introduces a few useful shorthands for tasks that in the past required multiple declarations. For example, `margin-inline` sets the `margin-left` and `margin-right` properties, while [`inset`](https://www.stefanjudis.com/today-i-learned/inset-is-a-shorthand-for-top-right-bottom-and-left/) sets the `top`, `right`, `bottom` and `left` properties.

```css
/* BEFORE */
main {
  margin-left: auto;
  margin-right: auto;
}

/* AFTER */
main {
  margin-inline: auto;
}
```

A website can add support for an RTL (right-to-left) layout by replacing all instances of `left` and `right` with their logical counterparts in the site’s CSS code. Switching to logical CSS makes sense for all websites because the user may translate the site to a language that is [written right-to-left](https://en.wikipedia.org/wiki/Writing_system#Directionality) using a machine translation service. The biggest languages with RTL scripts are Arabic ([310 million](https://en.wikipedia.org/wiki/Arabic) native speakers), Persian ([70 million](https://en.wikipedia.org/wiki/Persian_language)), and Urdu ([70 million](https://www.britannica.com/topic/Urdu-language)).

```css
/* switch to RTL when Google translates the page to an RTL language */
.translated-rtl {
  direction: rtl;
}
```

David Bushell’s personal website now [uses](https://dbushell.com/2021/02/02/changing-css-for-good-logical-properties-and-values/) logical CSS and relies on Google’s `translated-rtl` class to toggle the site’s [inline base direction](https://drafts.csswg.org/css-writing-modes-3/#inline-base-direction). Try translating David’s website to an RTL language in Chrome and compare the RTL layout with the site’s default LTR layout.

# Chrome ships three controversial Fugu APIs

Last week Chrome [shipped](https://blog.chromium.org/2021/01/chrome-89-beta-advanced-hardware.html) three web APIs for “advanced hardware interactions”: the WebHID and Web Serial APIs on desktop, and Web NFC on Android. All three APIs are part of Google’s capabilities project, also known as [Project Fugu](https://fugu-tracker.web.app/), and were developed in W3C community groups (they’re not web standards).

- The **WebHID API** allows web apps to connect to old and uncommon [human interface devices](https://en.wikipedia.org/wiki/Human_interface_device) that don’t have a compatible device driver for the operating system (e.g., Nintendo’s [Wii Remote](https://medium.com/samsung-internet-dev/wiimote-on-the-web-using-webhid-8ee6a0dcd4f3)).

- The **Web Serial API** allows web apps to communicate (“byte by byte”) with peripheral devices, such as microcontrollers (e.g., the [Arduino DHT11](https://twitter.com/kalanyei/status/1368124073138548736) temperature/humidity sensor) and 3D printers, through an [emulated](https://firt.dev/notes/chrome/#chrome-89) serial connection.

- **Web NFC** allows web apps to wirelessly read from and write to [NFC tags](https://web.dev/nfc/#terminology) at short distances (less than 10 cm).

Apple and Mozilla, the developers of the other two major browser engines, are currently opposed to these APIs. Apple has [decided](https://webkit.org/tracking-prevention/#anti-fingerprinting) to “not yet implement due to fingerprinting, security, and other concerns.” Mozilla’s concerns are summarized on the [Mozilla Specification Positions](https://mozilla.github.io/standards-positions/) page.

<figure>
  <img src="/media/web-api-controversy.png" alt="">
  <figcaption><a href="https://webapicontroversy.com/">webapicontroversy.com</a></figcaption>
</figure>

# Stretching SVG with `preserveAspectRatio=none`

By default, an SVG graphic scales to fit the `<svg>` element’s content box, while maintaining the aspect ratio defined by the `viewBox` attribute. In some cases, the author may want to stretch the SVG graphic so that it completely fills the content box on both axes. This can be achieved by setting the `preserveAspectRatio` attribute to `none` on the `<svg>` element.

INSERT VIDEO - /media/svg-preserveaspectratio-none.mp4

INSERT CODEPEN - https://codepen.io/simevidas/full/RwoERGM

Distorting SVG in this manner may seem [counterintuitive](https://buttondown.email/viewBox/archive/box-7-telescopes-mysteries-and-presents/), but disabling the aspect ratio via the `preserveAspectRatio=none` value can make sense for simple, decorative SVG graphics on a responsive web page:

> This value can be useful when you are using a path for a border or to add a little effect on a section (like a diagonal [line]), and you want the path to fill the space.

# WordPress tones down the use of italics

An italic font can be used to highlight important words (`<em>` element), titles of creative works (`<cite>`), technical terms, foreign phrases (`<i>`), and more. Italics are helpful when used discreetly in this manner, but long sections of italic text are considered an accessibility issue and should be [avoided](https://core.trac.wordpress.org/ticket/47327).

> Italicized text can be difficult to read for some people with dyslexia or related forms of reading disorders.

<figure>
  <img src="/media/italics-accessibility-issue.png" width="476" height="218" alt="">
  <figcaption>Putting the entire help text in italics is not recommended</figcaption>
</figure>

WordPress 5.7, which was [released](https://wordpress.org/news/2021/03/esperanza/) earlier this week, [removed](https://wordpress.org/news/2021/02/wordpress-5-7-beta-2/) italics on descriptions, help text, labels, error details text, and other places in the WordPress admin to “improve accessibility and readability.”

# Still no progress on CSS custom media queries

The CSS Media Queries Level 5 module specifies a [`@custom-media` rule](https://drafts.csswg.org/mediaqueries-5/#custom-mq) for defining custom media queries. This proposed feature was originally added to the CSS spec almost seven years ago (in [June 2014](https://www.w3.org/TR/2014/WD-mediaqueries-4-20140605/#custom-mq)) and has since then not been further developed nor received any interest from browser vendors.

```css
@custom-media --narrow-window (max-width: 30em);

@media (--narrow-window) {
  /* narrow window styles */
}
```

> A media query used in multiple places can instead be assigned to a custom media query, which can be used everywhere, and editing the media query requires touching only one line of code.

Custom media queries may not ship in browsers for quite some time, but websites can start using this feature today via the official [PostCSS plugin](https://github.com/postcss/postcss-custom-media) (or [PostCSS Preset Env](https://github.com/csstools/postcss-preset-env)) to reduce code repetition and make media queries [more readable](https://twitter.com/argyleink/status/1356651962754760705).

On a related note, there is also the idea of [author-defined environment variables](https://twitter.com/AmeliasBrain/status/1368790507036364801), which (unlike custom properties) could be used in media queries, but this potential feature has not yet been fully fleshed out in the CSS spec.

```css
@media (max-width: env(--narrow-window)) {
  /* narrow window styles */
}
```
