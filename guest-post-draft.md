# Weekly news: Feature Policy, ECMAScript `Intl` API, packaged PWAs

`<EDITOR_INTRO>`  
Šime posts regular content for web developers on [webplatform.news](https://webplatform.news).  
`</EDITOR_INTRO>`

## New Feature Policy API in Chrome

[Pete LePage](https://developers.google.com/web/updates/2019/04/nic74): You can use the `document.featurePolicy.allowedFeatures` method in Chrome to get a list of all Feature Policy-controlled features that are allowed on the current page.

![](/media/feature-policy-allowed-features.png)

**Note:** This API can be useful when implementing a feature policy (and updating an existing feature policy) on your website.

1. Open your site in Chrome and run the API in the JavaScript console to check which Feature Policy-controlled features are allowed on your site.

2. Read about individual features on [featurepolicy.info](https://featurepolicy.info/) and decide which features should be disabled (`'none'` value), and which features should be disabled only in cross-origin `<iframe>`s (`'self'` value).

3. Add the `Feature-Policy` header to your site’s HTTP responses (policies are separated by semicolons).

   ```http
   Feature-Policy: geolocation 'self';sync-xhr 'none'
   ```

4. Repeat step 1 to confirm that your new feature policy is in effect. You can also scan your site on [securityheaders.com](https://securityheaders.com/).

   ![](/media/security-headers-feature-policy.png)

## Other news

- [Dave Camp](https://blog.mozilla.org/blog/2019/06/04/firefox-now-available-with-enhanced-tracking-protection-by-default/): Firefox now blocks **cookies from known trackers** by default (when the cookie is used in a third-party context). This change is currently in effect only for new Firefox users; existing users will be automatically updated to the new policy “in the coming months.”

- [Pete LePage](https://developers.google.com/web/updates/2019/06/nic75): Chrome for Android now allows websites to **share images** (and other file types) via the `navigator.share` method. (Ed. note: See [issue 1014](https://webplatform.news/issues/2019-05-10) for more information about the Web Share API).

- [Valerie Young](https://bocoup.com/blog/widening-the-web-with-ecma-402): The ECMAScript **Internationalization APIs** for date and time formatting (`Intl.DateTimeFormat` constructor), and number formatting (`Intl.NumberFormat` constructor) are widely supported in browsers.

- [Alan Jeffrey](https://blog.mozvr.com/pathfinder-a-first-look/): Patrick Walton from Mozilla is working on a vector graphics renderer that can **render text smoothly at all angles** when viewed with an AR (Augmented Reality) headset. We plan to use it in our browsers for AR headsets (Firefox Reality).

- [Pinterest Engineering](https://medium.com/@Pinterest_Engineering/building-the-pinterest-app-for-windows-10-5e29f2146f7d): Our progressive web app is now available as a standalone desktop application on Windows 10. It can be installed via the Microsoft Store, which “treats the **packaged PWA** as a first class citizen with access to Windows 10 feature APIs.”

- [Jonathan Davis](https://webkit.org/blog/8967/release-notes-for-safari-technology-preview-83/): The **CSS `display: flow-root` value** has landed in Safari Technology Preview. (Ed. note: This value is already supported in Chrome and Firefox. See [issue 871](https://webplatform.news/issues/2017-04-05) for a use case.)
