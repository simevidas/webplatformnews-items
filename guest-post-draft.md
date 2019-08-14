# Weekly news: HTML `loading` attribute, the main ARIA specifications, moving from `<iframe>` to Shadow DOM

## Chrome ships the `loading` attribute

The HTML `loading` attribute for lazy-loading images and iframes is now supported in Chrome. You can add `loading="lazy"` to <mark>defer the loading of images</mark> and iframes that are _below_ the viewport until the user scrolls near them.

Google suggests either treating this feature as a progressive enhancement or using it on top of your existing JavaScript-based lazy-loading solution.

**Note:** This feature has not yet been added to the HTML Standard (but there is an [open pull request](https://github.com/whatwg/html/pull/3752)), and multiple links to Google’s documentation are listed on its [Chrome Status page](https://www.chromestatus.com/feature/5645767347798016).

**Source:** “[Native lazy-loading for the web](https://web.dev/native-lazy-loading)” by Google

## Overview of ARIA specifications

The main accessibility specifications for web developers:

<table>
<thead>
<tr>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><a href="https://w3c.github.io/html-aria/">ARIA in HTML</a></td>
<td>defines which ARIA role, state, and property attributes are allowed on which HTML elements (the implicit ARIA semantics are defined here)</td>
</tr>
<tr>
<td><a href="https://w3c.github.io/using-aria/">Using ARIA</a></td>
<td>provides practical advice on how to use ARIA in HTML, with an emphasis on dynamic content and advanced UI controls (the “five rules of ARIA use” are defined here)</td>
</tr>
<tr>
<td><a href="https://w3c.github.io/aria/">ARIA</a> (Accessible Rich Internet Applications)</td>
<td>defines the ARIA roles, states, and properties</td>
</tr>
<tr>
<td><a href="https://w3c.github.io/aria-practices/">ARIA Authoring Practices</a></td>
<td>provides general guidelines on how to use ARIA to create accessible apps (includes ARIA implementation patterns for common widgets)</td>
</tr>
<tr>
<td><a href="https://w3c.github.io/html-aam/">HTML Accessibility API Mappings</a></td>
<td>defines how browsers map HTML elements and attributes to the operating system’s accessibility APIs</td>
</tr>
<tr>
<td><a href="https://w3c.github.io/wcag/21/guidelines/">WCAG</a> (Web Content Accessibility Guidelines)</td>
<td>provides guidelines for making web content more accessible (success criteria for WCAG conformance are defined here)</td>
</tr>
</tbody></table>                                                            |

**Related:** “[Contributing to the ARIA Authoring Practices Guide](https://bocoup.com/blog/contributing-to-the-aria-authoring-practices-guide)” by Simon Pieters and Valerie Young

## Shadow DOM on BBC’s website

The BBC has moved from `<iframe>` to Shadow DOM for the embedded interactive visualizations on its website. This has resulted in significant improvements in load performance (“more than 25% faster”).

The available Shadow DOM polyfills didn’t reliably prevent styles from leaking across the Shadow DOM boundary, so they decided to instead fall back to `<iframe>` in browsers that don’t support Shadow DOM.

> Shadow DOM … can deliver content in a similar way to iframes in terms of encapsulation but without the negative overheads … We want encapsulation of an element whose content will appear seamlessly as part of the page. Shadow DOM gives us that without any need for a custom element.

One major drawback of this new approach is that CSS media queries can no longer be used to conditionally apply styles based on the content’s width (since the content no longer loads in a separate, embedded document).

> With iframes, media queries would give us the width of our content; with Shadow DOM, media queries give us the width of the device itself. This is a huge challenge for us. We now have no way of knowing how big our content is when it’s served.

**Source:** “[Goodbye iframes](https://medium.com/bbc-design-engineering/goodbye-iframes-6c84a651e137)” by Toby Cox

## Other news

- The next version of Chrome will introduce the **Largest Contentful Paint** performance metric; this new metric is a more accurate replacement for First Meaningful Paint, and it measures when the largest element is rendered in the viewport (usually, the largest image or paragraph of text) — **[source](https://twitter.com/philwalton/status/1159505273033089024)**

- Microsoft has created a prototype of a new tool for viewing a web page’s **DOM in 3D**; this tool is now experimentally available in the preview version of Edge — **[source](https://twitter.com/EdgeDevTools/status/1158485601798119424)**

- **Tracking prevention** has been enabled by default in the preview versions of Edge; it is set to balanced by default, which “blocks malicious trackers and some third-party trackers” — **[source](https://techdows.com/2019/08/microsoft-enables-tracking-prevention-by-default-in-new-microsoft-edge.html)**

Read more news in my new, weekly **Sunday issue**. Visit [webplatform.news](https://webplatform.news) for more information.
