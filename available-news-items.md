- The mobile version of Google Search includes AMP results on search results pages. When the user taps on an AMP result, the AMP page loads from Google’s domain (`google.com`) and is displayed in the [AMP Viewer](https://developers.google.com/search/docs/guides/about-amp).

  ![](/media/amp-viewer.png)

  Google Search now supports an alternative: If a website signs its AMP pages, and the visitor uses Chrome for Android, then tapping on an AMP result instead loads the <mark>signed version of the AMP page</mark> from Google’s servers, but to the user it appears as if they have navigated to the website normally.

  ![](/media/signed-exchange.png)

  The technology that enables this is called [Signed HTTP Exchanges](https://developers.google.com/web/updates/2018/11/signed-exchanges) (SXG). See the [announcement](https://webmasters.googleblog.com/2019/04/instant-loading-amp-pages-from-your-own.html) on Google Webmaster Central Blog for more details. The [specification](https://tools.ietf.org/html/draft-yasskin-http-origin-signed-responses-05) describes the following use case:

  > In order to speed up loading but still maintain control over its
  > content, an HTML page in a particular origin “O.com” could tell
  > clients to load its subresources from an intermediate content
  > distributor that’s not authoritative, but require that those
  > resources be signed by “O.com” so that the distributor couldn’t
  > modify the resources.

  Websites can add support for signed exchanges by running [AMP Packager](https://amp.dev/documentation/guides-and-tutorials/optimize-and-measure/signed-exchange) on the server side. Cloudflare has launched a free feature called “[AMP Real URL](https://blog.cloudflare.com/announcing-amp-real-url/)” that fully automates the signing process for AMP pages served from its CDN.

- [Malte Ubl](https://mobile.twitter.com/cramforce/status/1118432194324725761): “Bento AMP” is the name of an ongoing effort to unbundle AMP web components from AMP and make them <mark>usable in all web pages</mark> (for more info, see “What’s next in AMP” at [11:21](https://youtu.be/rx74ySmQFXs?t=681)).

  ![](/media/bento-amp.png)

- [Weston Ruter](https://mobile.twitter.com/westonruter/status/1118153761342418952): The size of WordPress’s default theme (Twenty Nineteen) increased substantially in version 5.1, which broke AMP compatibility (AMP limits the amount of CSS to 50 KB). In response, we’ve made improvements to the <mark>CSS tree shaker</mark> in the AMP plugin for WordPress; we were able to cut the amount of CSS by more than half (from 70 KB to 33 KB).

  > To achieve these improvements in Twenty Nineteen, style processing was improved in the following ways:
  >
  > - Add tree shaking for attribute selectors
  > - Add tree shaking for `:lang()` selectors
  > - Expand externalization of `data:` URLs in `@font-face` rules

- [Tab Atkins](https://mobile.twitter.com/tabatkins/status/1117942439262572544): When using the CSS `linear-gradient()` function, you can adjust the <mark>midpoint of the gradient</mark> by inserting a percentage (or length) value, called a “[color interpolation hint](https://drafts.csswg.org/css-images-4/#color-stop-syntax),” between the two color values.

  ```css
   {
    /* midpoint defaults to 50% */
    background: linear-gradient(#fff, #bbf);

    /* midpoint set to 80% */
    background: linear-gradient(#fff, 80%, #bbf);
  }
  ```

  ![](/media/gradient-midpoint-adjustment.png)

- [Lyndon NA](https://mobile.twitter.com/darth_na/status/1118252251452145664): The `details` property of mouse events (incl. `mousedown` and `click`) returns the <mark>current click count</mark>.

  <video controls playsinline src="/media/click-count.mp4"></video>

  **Note:** This feature is defined in the UI Events specification ([section 4.3.1.2](https://w3c.github.io/uievents/#current-click-count)). Browsers reset the click count after about 500 ms.

  > The current click count [is] a non-negative integer indicating the number of consecutive clicks of a pointing device button within a specific time. The delay after which the count resets is specific to the environment configuration.

- [Will Boyd](https://mobile.twitter.com/AmeliasBrain/status/1118630988488200192): When the user navigates back to the previous web page, browsers restore the scroll position but often the <mark>tab position is reset</mark> (the visited link is not focused). This impairs the user experience of keyboard users.

- [Elizabeth Schafer](https://dev.to/elizabethschafer/designing-button-focus-states-for-better-usability-gm2): Don’t forget to <mark>style the `:focus` state</mark> when designing buttons in CSS. Users who navigate the page with the keyboard, rely on this state to know where they are on the page.

  > If the focus state isn't visible (or hard to see), it's like trying to use a website with an invisible mouse cursor.

- [Fastly](https://mobile.twitter.com/fastly/status/1111018048243355649): <mark>HTTP trailers</mark> (or HTTP trailing headers) are headers that are sent after the body has already been sent. Firefox supports the `Server-Timing` trailer since version 64 (December 2018). A web server can use this trailer to report to the web app how long it took for the response to be delivered.

- [Navid Zolghadr](https://discourse.wicg.io/t/proposal-new-events-for-overscroll-and-scrollend/3481): The proposed <mark>`overscroll` and `scrollend` events</mark> would make it easier to implement custom scroll boundary behaviors when the user scrolls against the edge of a scrollport (the visual viewport of a scroll container).

- [Google Webmasters](https://webmasters.googleblog.com/2019/04/user-experience-improvements-with-page.html): You can use Chrome’s Network Error Logging feature (HTTP `NEL` response header) to measure the <mark>abandonment rate</mark> for navigations to your website.

  ```http
  Report-To: {"group": "default", "max_age": 31536000,
      "endpoints": [{"url": "https://foo.report-uri.com/a/d/g"}]}
  NEL: {"report_to": "default", "max_age": 31536000}
  ```

  **Note:** The specification defines a total of [29 network error types](https://w3c.github.io/network-error-logging/#predefined-network-error-types), incl. `tcp.aborted`, `http.error`, and `abandoned`.

- [Johann Hofmann](https://blog.nightly.mozilla.org/2019/04/01/reducing-notification-permission-prompt-spam-in-firefox/): According to Mozilla’s telemetry data, users almost unanimously reject <mark>unsolicited permission requests</mark> to allow notifications from websites. Firefox may in the future reject these prompts automatically (and instead just show an icon in the address bar).

  > As a general principle, prompting for permissions should be done based on user interaction. Offering your users additional context, and delaying the prompt until the user chooses to show it, will not only future-proof your site, but likely also increase your user engagement and prompt acceptance rates.

- [Andrew Betts](https://www.fastly.com/blog/feature-policy-webs-missing-guardrails): Websites can use the HTTP `Feature-Policy` response header to prevent third parties from secretly using powerful features such as geolocation, and to <mark>disable certain bad practices</mark> (e.g., `document.write`, parser-blocking JavaScript, unoptimized images).

  > This allows good practices to be more easily rewarded. … Search results could be badged with some approving “fast” logomark or (more controversially perhaps) get a higher result ranking if they disallow themselves certain policy-controlled behaviours.

  **Note:** Feature Policy is an emerging technology. See [featurepolicy.info](https://featurepolicy.info/) for more information about individual policies and their level of support in browsers.

- [Henrik Joreteg](https://mobile.twitter.com/HenrikJoreteg/status/1111853724081610753): On iOS, several important APIs are limited to Safari and are not available in any of the <mark>alternative iOS browsers</mark>. These include service workers, web payments, and camera access.

  **Note:** Chrome for iOS supports web payments via a [custom implementation](https://nielsleenheer.com/articles/2017/about-chrome-ios-and-payment-request/). I’ve created a [browser support table](https://html5test.com/compare/browser/ac70c543eaf34147/47955043eaf4e9aa/13c1af43eafb15e8/c509b443eaff324e/6d0d3d43eb01ac6b.html) on HTML5test that highlights the differences between some of the popular iOS browsers.

  ![](/media/ios-browser-support-table.png)

- [Stefan Zager](https://groups.google.com/a/chromium.org/d/msg/blink-dev/m-UwqK3cdjA/OHds_wERAwAJ): The proposed `requestPostAnimationFrame` function, which closely mirrors `requestAnimationFrame`, would allow developers to receive a callback immediately _after_ the <mark>next rendering update</mark>. I intend to implement this API in Chromium.

  > `requestPostAnimationFrame` provides a way to get the earliest possible start on preparing for the next rendering update, without any possibility of the work being preempted by other less critical tasks.

  > Because `requestPostAnimationFrame` handlers run immediately after the rendering update, before any other code, it is guaranteed that layout will be clean, and querying layout information will not force an additional synchronous layout.

- [Andrey Sitnik](https://mobile.twitter.com/sitnikcode/status/1110759704454721536): You can run `npx autoprefixer --info` in your project to check which <mark>CSS vendor prefixes</mark> are still required for your target browsers according to your Browserslist config (or the [default browsers](https://github.com/browserslist/browserslist#queries) if you don’t specify one).
