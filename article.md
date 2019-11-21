# Weekly Platform News: Contrast Ratio Range, `replaceAll` Method, Native File System API

## Firefox shows the contrast ratio range for text on a multicolored background

According to [Success Criterion 1.4.3](https://w3c.github.io/wcag/21/guidelines/#contrast-minimum) of the Web Content Accessibility Guidelines (WCAG), text should have a contrast ratio of at least 4.5. (A lower contrast ratio is acceptable only if the text is `24px` or larger.)

If the background of the text is not a solid color but a color gradient or photograph, you can use the special element picker in Firefox’s Accessibility panel to get a range of contrast ratios based on the element’s actual background.

<video controls src="/media/firefox-accessibility-picker.mp4"></video>

<small>(via [Šime Vidas](https://twitter.com/simevidas/status/1181941591826685954))</small>

## Replacing all instances of a substring in a string

The new JavaScript `replaceAll` method makes it easier to replace all instances of a substring in a string without having to convert the substring to a regex first, which is “hard to get right since JavaScript doesn’t offer a built-in mechanism to escape regular expression patterns.”

```js
// BEFORE
str = str.replace(/foo/g, "bar");

// AFTER
str = str.replaceAll("foo", "bar");
```

Note: This new string method has not yet shipped in browsers, but you can start using it today via Babel (it’s automatically polyfilled by [@babel/preset-env](https://babeljs.io/docs/en/babel-preset-env)).

<small>(via [Mathias Bynens](https://twitter.com/mathias/status/1193917548875501568))</small>

## Try out the Native File System API in Chrome

The Native File System API, which is [experimentally supported in Chrome](https://groups.google.com/a/chromium.org/d/msg/blink-dev/noan0cgEBGQ/t8DuK8_hDwAJ), allows web apps to read or save changes directly to local files on the person’s computer. The app is granted permission to view and edit files in a specific folder [via two separate prompts](https://twitter.com/simevidas/status/1196243432554950656).

![](/media/file-system-prompt.png)

You can try out this new feature by visiting [labs.vaadin.com](https://labs.vaadin.com/native-fs/) in Chrome on desktop.

<small>(via [Thomas Steiner](https://twitter.com/tomayac/status/1194715245781979136))</small>

## More news…

![](/media/sunday-issue-18.png)

Read more news in my weekly newsletter for web developers. Pledge as little as \$2 per month to get the latest news from me via email every Monday.

<a href="https://www.patreon.com/posts/sunday-issue-18-31699106" class="button">More News →</a>
