# Weekly news: Mozilla WebThings, Internet Explorer mode, GraphQL

`<EDITOR_INTRO>`  
Šime posts regular content for web developers on [webplatform.news](https://webplatform.news).  
`</EDITOR_INTRO>`

## Mozilla WebThings provides complete privacy for user data

[Josephine Lau](https://mobile.twitter.com/mozhacks/status/1129451585686441987): Smart home companies require that users’ data goes through their servers, which means that people are giving up their privacy for the convenience of a smart home device (e.g., smart light bulb).

> We’ve learned that people are concerned about the privacy of their smart home data. And yet, when there’s no alternative, they feel the need to trade away their privacy for convenience.

Mozilla WebThings is an alternative approach to the Internet of Things that stores user data in the user’s home. Devices can be controlled locally via a web interface, and the data is tunneled through a private HTTPS connection.

![A diagram showing how Mozilla doesn’t store user data in the cloud, unlike smart home vendors](/media/mozilla-webthings-framework.png)

## An Internet Explorer mode is coming to Edge

[Fred Pullen](https://mobile.twitter.com/MSEdgeDev/status/1129505305719496704): The next version of Edge will include an Internet Explorer mode for backward compatibility with legacy websites. Edge will also for the first time be available on older versions of Windows (incl. Windows 7 and 8.1).

> By introducing Internet Explorer mode, we’re effectively blurring the lines between the browsers. From an end-user standpoint, it seems like a single browser. … You can use IE mode to limit the sites that instantiate Internet Explorer just to the sites that you approved.

<video controls src="/media/edge-ie-mode.mp4"></video>

## Other interesting articles

- [Introducing the first Microsoft Edge preview builds for macOS](https://blogs.windows.com/msedgedev/2019/05/20/microsoft-edge-macos-canary-preview/)

  Edge Canary (analogous to Chrome Canary) is now officially available on macOS. This version of Edge updates daily.

  > With our new Chromium foundation, you can expect a consistent rendering experience across the Windows and macOS versions of Microsoft Edge.

- [#EmberJS2019 More Accessible Than Ever](https://yehudakatz.com/2019/05/20/ember-2019/)

  > Navigating from one page to another in a client-side web app provides no feedback by default in virtually all popular routing solutions across the client-side ecosystem.

  Their goal is to make Ember’s router more accessible and screen reader friendly.

- [Opinion: Five developer trends to watch in 2019](https://www.developer-tech.com/news/2019/may/16/opinion-five-developer-trends-2019/)

  The article includes a good, short explanation of what GraphQL is and what problems it solves.

- [Part 2: What the Fr(action)?](https://css-irl.info/debugging-css-grid-part-2-what-the-fraction/)

  Read the last section (“Intrinsic and extrinsic sizing“). All three columns have the size `1fr` but the middle one is wider because of its content. This can be prevented by using the size `minmax(0, 1fr)` instead.

- [Parallel streaming of progressive images](https://blog.cloudflare.com/parallel-streaming-of-progressive-images/)

  Instead of loading from top to bottom, progressive images appear blurry at first and become sharper as more data loads.

  > The benefits of progressive rendering are unique to JPEG (supported in all browsers) and JPEG 2000 (supported in Safari). GIF and PNG have interlaced modes, but these modes come at a cost of worse compression. WebP doesn't even support progressive rendering at all. This creates a dilemma: WebP is usually 20%-30% smaller than a JPEG of equivalent quality, but progressive JPEG appears to load 50% faster.
