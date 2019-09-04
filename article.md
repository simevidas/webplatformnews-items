# Weekly news: “Text Spacing” bookmarklet, top-level `await`, AMP’s new loading indicator

## Check if your content breaks after increasing text spacing

Dylan Barrell from Deque has created a bookmarklet that you can use to check if there are any issues with the content or functionality of your website after increasing the line, paragraph, letter, and word spacing, according to the [“Text Spacing” success criterion](https://w3c.github.io/wcag/21/guidelines/#text-spacing) of the Web Content Accessibility Guidelines.

<video src="/media/text-spacing-bookmarklet.mp4" controls></video>

<small>(via [Dylan Barrell](https://twitter.com/dylanbarrell/status/1163474668822630401))</small>

## Using top-level `await` in JavaScript modules

The proposed top-level `await` feature is especially useful in JavaScript modules: If module A uses top-level `await` (e.g., to connect to a database), and module B imports module A — via the `import` declaration — then the body of B will be evaluated after the body of A (i.e., B will correctly wait for A).

> Top-level `await` enables modules to act as big async functions: With top-level `await`, ECMAScript Modules (ESM) can `await` resources, causing other modules who `import` them to wait before they start evaluating their body.

<small>(via [Brian Kardell](https://bkardell.com/blog/TopLevelAwaitIn2m.html))</small>

## AMP’s new multi-stage loading indicator

AMP has created a new multi-stage loading indicator that has better perceived performance (tested on 2,500 users): It shows nothing until 0.5 s, then an intermediate animation until 3.5 s, and finally a looping spinner after that.

![](/media/amp-loading-indicator.png)

<small>(via [Andrew Watterson](https://blog.amp.dev/2019/08/26/making-your-wait-a-little-more-great-new-loading-indicators-in-amp/))</small>

## In other news…

- AMP has released the `<amp-script>` element which, for the first time, allows AMP pages to add custom JavaScript, with some constraints: The code runs in a separate worker thread and requires a user gesture to change page content (via [AMP Project](https://twitter.com/AMPhtml/status/1164245170868641794)).

- The HTML Standard has made `autofocus` a global attribute that “applies to all elements, not just to form controls” (e.g., this change enables `<div contenteditable autofocus>`, but no browser supports this yet) (via [Kent Tamura](https://github.com/whatwg/html/commit/f5ae47e538b6d21aa3ea6c70ab6966f4d40c4620)).

- Facebook’s in-app browser (powered by Android's WebView) is not a browser: “Facebook is breaking the web for 20–30% of your traffic because you aren't demanding they do better” (via [Alex Russell](https://twitter.com/slightlylate/status/1167521819789627392)).

Read more news in my new, weekly **Sunday issue**. Visit [webplatform.news](https://webplatform.news) for more information.
