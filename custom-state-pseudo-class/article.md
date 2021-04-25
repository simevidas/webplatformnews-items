# Custom state pseudo-classes in Chrome

There is an increasing number of “custom” features on the web platform. We have custom properties (`--my-property`), custom elements (`<my-element>`), and custom events (`new CustomEvent('myEvent')`). At one point, we might even get [custom media queries](https://css-tricks.com/platform-news-defaulting-to-logical-css-fugu-apis-custom-media-queries-and-wordpress-vs-italics/#still-no-progress-on-css-custom-media-queries) (`@media (--my-media)`).

But that’s not all! You might have missed it because it wasn’t mentioned in Google’s “[New in Chrome 90](https://developer.chrome.com/blog/new-in-chrome-90/)” article (to be fair, [declarative shadow DOM](https://css-tricks.com/platform-news-using-focus-visible-bbcs-new-typeface-declarative-shadow-doms-a11y-and-placeholders/#declarative-shadow-dom-could-help-popularize-style-encapsulation) stole the show in this release), but Chrome just added support for yet another “custom” feature: custom state pseudo-classes (`:--my-state`). Read on to find out what this feature is all about.

## Built-in states

Before talking about custom states, let’s take a quick look at the built-in states that are defined for built-in HTML elements. The [CSS Selectors module](https://drafts.csswg.org/selectors/) and the [“Pseudo-classes” section](https://html.spec.whatwg.org/multipage/semantics-other.html#pseudo-classes) of the HTML Standard specify a number of pseudo-classes that can be used to match elements in different states. The following pseudo-classes are all widely supported in today’s browsers:

<table>
    <tr>
        <th colspan=2><strong>User action</strong></th>
    </tr>
    <tr>
        <td><code>:hover</code></td>
        <td>the mouse cursor hovers over the element</td>
    </tr>
    <tr>
        <td><code>:active</code></td>
        <td>the element is being activated by the user</td>
    </tr>
    <tr>
        <td><code>:focus</code></td>
        <td>the element has the focus</td>
    </tr>
    <tr>
        <td><code>:focus-within</code></td>
        <td>the element has or contains the focus</td>
    </tr>
    <tr>
        <th colspan=2><strong>Location</strong></th>
    </tr>
    <tr>
        <td><code>:visited</code></td>
        <td>the link has been visited by the user</td>
    </tr>
    <tr>
        <td><code>:target</code></td>
        <td>the element is targeted by the page URL’s fragment</td>
    </tr>
    <tr>
        <th colspan=2><strong>Input</strong></th>
    </tr>
    <tr>
        <td><code>:disabled</code></td>
        <td>the form element is disabled</td>
    </tr>
    <tr>
        <td><code>:placeholder-shown</code></td>
        <td>the input element is showing placeholder text</td>
    </tr>   
    <tr>
        <td><code>:checked</code></td>
        <td>the checkbox or radio button is selected</td>
    </tr>
    <tr>
        <td><code>:invalid</code></td>
        <td>the form element’s value is invalid</td>
    </tr>
    <tr>
        <td><code>:out-of-range</code></td>
        <td>the input element’s value is <a href="https://twitter.com/mgechev/status/1384726124522098688">outside the specificed range</a></td>
    </tr>
    <tr>
        <td><code>:-webkit-autofill</code></td>
        <td>the input element has been autofilled by the browser</td>
    </tr>
    <tr>
        <th colspan=2><strong>Other</strong></th>
    </tr>
    <tr>
        <td><code>:defined</code></td>
        <td>the custom element has been registered</td>
    </tr>
</table>

**Note:** For brevity, some pseudo-classes have been omitted, and some descriptions don’t mention every possible use-case.

## Custom states

Like built-in elements, custom elements can have different states. A web page that uses a custom element may want to style these states. The custom element could expose its states via CSS classes (`class` attribute) on its host element, but that’s [considered an anti-pattern](https://github.com/WICG/webcomponents/issues/738#issuecomment-367499244).

Chrome now supports an API for adding internal states to custom elements. These custom states are exposed to the outer page via custom state pseudo-classes. For example, a page that uses a `<live-score>` element can declare styles for that element’s custom `--loading` state.

```css
live-score {
  /* default styles for this element */
}

live-score:--loading {
  /* styles for when new content is loading */
}
```

## Let’s add a `--checked` state to a `<labeled-checkbox>` element

The [Custom State Pseudo Class](https://wicg.github.io/custom-state-pseudo-class/) specification contains a complete code example, which I will use to explain the API. The JavaScript portion of this feature is located in the custom element‘s class definition. In the constructor, an “[element internals](https://html.spec.whatwg.org/multipage/custom-elements.html#element-internals)” object is created for the custom element. Then, custom states can be set and unset on the internal `states` object.

**Note:** The [`ElementInternals`](https://html.spec.whatwg.org/multipage/custom-elements.html#element-internals) API ensures that the custom states are [read-only](https://github.com/w3ctag/design-reviews/issues/428#issuecomment-566103510) to the outside. In other words, the outer page cannot modify the custom element’s internal states.

```js
class LabeledCheckbox extends HTMLElement {
  constructor() {
    super();

    // 1. instantiate the element’s “internals”
    this._internals = this.attachInternals();

    // (other code)
  }

  // 2. toggle a custom state
  set checked(flag) {
    if (flag) {
      this._internals.states.add("--checked");
    } else {
      this._internals.states.delete("--checked");
    }
  }

  // (other code)
}
```

The web page can now style the custom element’s internal states via custom pseudo-classes of the same name. In our example, the `--checked` state is exposed via the `:--checked` pseudo-class.

```css
labeled-checkbox {
  /* styles for the default state */
}

labeled-checkbox:--checked {
  /* styles for the --checked state */
}
```

<figure>
    <video src="custom-state-pseudo-class.mp4" controls>⚠️  The video could not be rendered</video>
    <figcaption>(<a href="https://codepen.io/simevidas/pen/ZELwEBy">Try the demo in Chrome</a>)</figcaption>
</figure>

## This feature is not (yet) a standard

Browser vendors have been debating for the [past three years](https://github.com/WICG/webcomponents/issues/738) how to expose the internal states of custom elements via custom pseudo-classes. Google’s [Custom State Pseudo Class](https://wicg.github.io/custom-state-pseudo-class/) specification remains an “unofficial draft” hosted by <abbr title="Web Incubator Community Group">WICG</abbr>. The feature [underwent a design review](https://github.com/w3ctag/design-reviews/issues/428) at the W3C <abbr title="Technical Architecture Group">TAG</abbr> and has been [handed over to the CSS Working Group](https://github.com/w3c/csswg-drafts/issues/4805). In Chrome’s ”intent to ship” discussion, [Mounir Lamouri wrote this](https://groups.google.com/a/chromium.org/g/blink-dev/c/dJibhmzE73o/m/VT-NceIhAAAJ):

> It looks like this feature has good support. It sounds that <mark>it may be hard for web developers to benefit from it as long as it’s not widely shipped</mark>, but hopefully Firefox and Safari will follow and implement it too. Someone has to implement it first, and given that there are no foreseeable backward incompatible changes, it sounds safe to go first.

We now have to wait for the implementations in Firefox and Safari. The browser bugs have been filed ([Mozilla bug 1588763](https://bugzilla.mozilla.org/show_bug.cgi?id=1588763) and [WebKit bug 215911](https://bugs.webkit.org/show_bug.cgi?id=215911)) but have not received much attention yet.
