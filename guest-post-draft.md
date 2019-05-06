# Weekly news: Feature Policy, Signed Exchanges, iOS browsers

`<EDITOR_INTRO>`  
Šime posts regular content for web developers on [webplatform.news](https://webplatform.news).  
`</EDITOR_INTRO>`

## Feature Policy in Chrome

[Andrew Betts](https://www.fastly.com/blog/feature-policy-webs-missing-guardrails): Websites can use the HTTP `Feature-Policy` response header to prevent third parties from secretly using powerful features such as geolocation, and to <mark>disable certain bad practices</mark> (e.g., `document.write`, parser-blocking JavaScript, unoptimized images).

> This allows good practices to be more easily rewarded. … Search results could be badged with some approving “fast” logomark or (more controversially perhaps) get a higher result ranking if they disallow themselves certain policy-controlled behaviours.

**Note:** Feature Policy is an emerging technology. See [featurepolicy.info](https://featurepolicy.info/) for more information about individual policies and their level of support in browsers.

## Signed exchanges on Google Search

The mobile version of Google Search includes AMP results on search results pages. When the user taps on an AMP result, the AMP page loads from Google’s domain (`google.com`) and is displayed in the [AMP Viewer](https://developers.google.com/search/docs/guides/about-amp).

![](/media/amp-viewer.png)

Google Search now supports an alternative: If a website signs its AMP pages, and the visitor uses Chrome for Android, then tapping on an AMP result instead loads the <mark>signed version of the AMP page</mark> from Google’s servers, but to the user it appears as if they have navigated to the website normally.

![](/media/signed-exchange.png)

The technology that enables this is called [Signed HTTP Exchanges](https://developers.google.com/web/updates/2018/11/signed-exchanges) (SXG). See the [announcement](https://webmasters.googleblog.com/2019/04/instant-loading-amp-pages-from-your-own.html) on Google Webmaster Central Blog for more details. The [specification](https://tools.ietf.org/html/draft-yasskin-http-origin-signed-responses-05) describes the following use case:

> In order to speed up loading but still maintain control over its content, an HTML page in a particular origin “O.com” could tell clients to load its subresources from an intermediate content distributor that’s not authoritative, but require that those resources be signed by “O.com” so that the distributor couldn’t modify the resources.

Websites can add support for signed exchanges by running [AMP Packager](https://amp.dev/documentation/guides-and-tutorials/optimize-and-measure/signed-exchange) on the server side. Cloudflare has launched a free feature called “[AMP Real URL](https://blog.cloudflare.com/announcing-amp-real-url/)” that fully automates the signing process for AMP pages served from its CDN.

## Alternative iOS browsers

[Henrik Joreteg](https://mobile.twitter.com/HenrikJoreteg/status/1111853724081610753): On iOS, several important APIs are limited to Safari and are not available in any of the <mark>alternative iOS browsers</mark>. These include service workers, web payments, and camera access.

**Note:** Chrome for iOS supports web payments via a [custom implementation](https://nielsleenheer.com/articles/2017/about-chrome-ios-and-payment-request/). I’ve created a [browser support table](https://html5test.com/compare/browser/ac70c543eaf34147/47955043eaf4e9aa/13c1af43eafb15e8/c509b443eaff324e/6d0d3d43eb01ac6b.html) on HTML5test that highlights the differences between some of the popular iOS browsers.

![](/media/ios-browser-support-table.png)
