# Weekly news: CSS `::marker` pseudo-element, pre-rendering web components, adding Webmention to your site

`<EDITOR_INTRO>`  
Šime posts regular content for web developers on [webplatform.news](https://webplatform.news).  
`</EDITOR_INTRO>`

## Using plain text fields for date input

[Adrian Roselli](http://adrianroselli.com/2019/07/maybe-you-dont-need-a-date-picker.html): Keyboard users prefer regular text fields over complex date pickers, and voice users are frustrated by the native control (`<input type="date">`).

> Previously, I have relied on plain text inputs as date fields with custom validation for the site, typically using the same logic on the client and the server. For known dates — birthdays, holidays, anniversaries, etc. — it has tested well.

## Pre-rendering web components

[Max Lynch](https://dev.to/ionic/why-we-use-web-components-2c1i): Stencil is a “web component compiler” that can be used to pre-render web components (incl. Shadow DOM) or hide them until they are fully styled to avoid the flash of unstyled content (FOUC).

This tool also makes sure that polyfills are only loaded when needed, and its Component API includes useful decorators and hooks that make writing web components easier (e.g., the `Prop` decorator handles changes to attributes).

```js
import { Component, Prop, h } from "@stencil/core";

@Component({
  tag: "my-component"
})
export class MyComponent {
  @Prop() age: number = 0;

  render() {
    return <div>I am {this.age} years old</div>;
  }
}
```

## The CSS `::marker` pseudo-element

[Rachel Andrew](https://www.smashingmagazine.com/2019/07/css-lists-markers-counters/): When the CSS `display: list-item` declaration is applied to an element, the element generates a marker box containing a marker, e.g., a list bullet (the `<li>` and `<summary>` elements have markers by default).

Markers can be styled via the `::marker` pseudo-element (useful for changing the color or font of the marker), but this CSS feature is currently only supported in Firefox.

![](/media/css-marker-pseudo-element.jpg)

## Adding Webmention to your website

[Daniel Aleksandersen](https://www.ctrl.blog/entry/setup-webmention.html):

1. Sign up on [Webmention.io](https://webmention.io/); this is a service that collects webmentions on your behalf.

2. Add `<link rel="webmention">` (with the appropriate `href` value) to your web pages.

   > There are also Webmention plugins available for all major content management systems (CMS) if you prefer building on top of your CMS.

3. Fetch webmentions from [Webmention.io](https://webmention.io/) (via Ajax) to display them on your page.

4. Use [webmention.app](https://webmention.app/) to automate sending webmentions (when you publish content that includes links to other sites that support Webmention).

   ![](/media/webmention-app.png)
