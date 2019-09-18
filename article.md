# Weekly platform news: Emoji string length, issues with rounded buttons, Bundled Exchanges

## The JavaScript string length of emoji characters

A single rendered emoji can have a JavaScript string length of up to `7` if it contains additional _Unicode scalar values_ that represent a skin tone modifier, gender specification, and multicolor rendering.

![](/media/emoji-string-length.png)

<small>(via [Henri Sivonen](https://hsivonen.fi/string-length/))</small>

## An accessibility issue with rounded buttons

Be aware that applying CSS `border-radius` to a `<button>` element reduces the button’s interactive area (“those lost corner pixels are no longer clickable”).

![](/media/button-rounded-corners.png)

You can avoid this accessibility issue in CSS, e.g., by emulating rounded corners via `border-image` instead, or by overlaying the button with an absolutely positioned, transparent `::before` element.

<small>(via [Tyler Sticka](https://twitter.com/tylersticka/status/1168917812288675842))</small>

## Sharing web pages while offline with Bundled Exchanges

Chrome plans to add support for navigation to Bundled Exchanges (part of Web Packaging). A _bundled exchange_ is a collection of HTTP request/response pairs, and it can be used to bundle a web page and all of its resources.

> The browser should be able to parse and verify the bundle’s signature and then navigate to the website represented by the bundle without actually connecting to the site as all the necessary subresources could be served by the bundle.

Kinuko Yasuda from Google has posted a video that demonstrates how Bundled Exchanges enable sharing web pages (e.g., a web game) with other devices while offline.

<small>(via [Kinuko Yasuda](https://twitter.com/kinu/status/1171332094347268096))</small>

---

![](/media/sunday-issue-9.png)

Read even more news in my weekly **Sunday issue**, which can be delivered to you via email every Monday morning. Visit [webplatform.news](https://webplatform.news) for more information.
