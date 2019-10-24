# Weekly Platform News: WebAPK Limited to Chrome, Discernible Focus Rectangles, Modal Window API

## WebAPKs are not available to Firefox on Android

On Android, both Chrome and Firefox have an “Add to home screen” option, but while Firefox merely adds a shortcut for the web app to the user’s home screen, Chrome actually installs the web app (as long as it meets the [PWA install criteria](https://developers.google.com/web/fundamentals/app-install-banners/#criteria)) via a [WebAPK](https://developers.google.com/web/fundamentals/integration/webapks).

Progressive Web Apps installed in such a way are added to the device’s app drawer, and URLs that are within the PWA’s scope (as specified in its manifest) open in the PWA instead of the default browser.

Tiger Oakes who is implementing PWA-related features at Mozilla, explains why Firefox cannot install PWAs on Android: “WebAPK is not available to us since we don’t own an app store like Google Play and Galaxy Apps.”

<small>(via [Tiger Oakes](https://twitter.com/Not_Woods/status/1185235124046032896))</small>

## More accessible focus rectangles are coming to Chrome and Edge

Microsoft and Google have made accessibility improvements to various form controls. The two main changes are the larger touch targets on the time and date inputs, and the redesigned focus rectangles that are now easily discernible on any background.

<video controls src="/media/improved-focus-rectangles.mp4"></video>

The updated form controls are available in the preview version of Edge. Mac users may have to manually enable the “Web Platform Fluent Controls” flag on the `about:flags` page.

<small>(via [Microsoft Edge Dev](https://twitter.com/MSEdgeDev/status/1184129651612028928))</small>

## A newly proposed API for loading third-parties in modal windows

The proposed Modal Window API would allow a website to load another website in a modal window (in a top-level browsing context) for the purposes of authentication, payments, sharing, access to third-party services, etc.

Only a single modal window would be allowed at a time, and the two websites could communicate with each other via message events (`postMessage` method).

This API is intended as a better alternative to existing methods, such as pop-ups, which can be confusing to users and blocked by browsers, and redirects, which cause the original context to be torn down and recreated (or completely lost in the case of an error in the third-party service).

<small>(via [Adrian Hope-Bailie](https://discourse.wicg.io/t/proposal-modal-window/3982))</small>

## More news…

![](/media/sunday-issue-14.png)

Read even more news in my weekly **Sunday issue** that can be delivered to you via email every Monday morning.

<a href="https://webplatform.news/issues/2019-08-30" class="button">More News →</a>
