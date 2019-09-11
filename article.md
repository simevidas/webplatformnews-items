# Weekly platform news: Apple deploys web components, progressive HTML rendering, self-hosting critical resources

## Apple deploys web components built using Stencil

The new Apple Music web app (beta) uses a JavaScript framework (Ember.js) but also standard web components such as `<apple-music-video-player>` that are built using Stencil, a web component compiler.

**Note:** Stencil is a build-time tool that generates standard web components with minimal overhead, while providing core features such as templating, state management, and routing, as well as performance features such as code-splitting and lazy-loading.

> Apple just deployed into production nearly 50 web components powering a major app they have a significant amount of revenue and strategic value riding on. You can’t say that “no one uses web components” or they are “solving problems that don‘t exist or have been solved better in user land” with a straight face anymore.

<small>(via [Max Lynch](https://dev.to/ionic/apple-just-shipped-web-components-to-production-and-you-probably-missed-it-57pf))</small>

## Instagram makes use of chunked transfer encoding and progressive HTML rendering

Instagram’s website uses HTTP chunked transfer encoding to stream the contents of the HTML document to the browser as each part of the page is generated on the server.

> We can flush the HTML `<head>` to the browser almost immediately … This allows the browser to start downloading scripts and stylesheets while the server is busy generating the dynamic data in the rest of the page.

They also use this technique to flush JSON data to the page in `<script>` elements. The client script waits for this data (using `Promise`) instead of requesting it via XHR.

<small>(via [Glenn Conner](https://instagram-engineering.com/making-instagram-com-faster-part-2-f350c8fba0d4))</small>

## Consider self-hosting your critical resources

One section of University of Notre Dame’s website used to load jQuery from Google’s CDN, which could result in very long loading times (100+ seconds) when visiting the site from China. They’ve resolved the issue by self-hosting jQuery instead.

![](/media/google-cdn-china.png)

<small>(via [Erik Runyon](https://erikrunyon.com/2019/09/render-blocking-resource/))</small>

---

![](/media/sunday-issue-8.png)

Read even more news in my weekly **Sunday issue**. Visit [webplatform.news](https://webplatform.news) for more information.
