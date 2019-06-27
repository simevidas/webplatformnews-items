# Weekly news: Event Timing, Google Earth for Web, undead session cookies

`<EDITOR_INTRO>`  
Šime posts regular content for web developers on [webplatform.news](https://webplatform.news).  
`</EDITOR_INTRO>`

## Tracking down slow event handlers with Event Timing

[Gilles Dubuc](https://phabricator.wikimedia.org/phame/live/7/post/168/tracking_down_slow_event_handlers_with_event_timing/): Event Timing is experimentally available in Chrome (as an Origin Trial), and Wikipedia is taking part in the trial. This API can be used to accurately determine the duration of event handlers with the goal of surfacing slow events.

> We quickly identified 3 very frequent slow click handlers experienced frequently by real users on Wikipedia. … Two of those issues are caused by expensive JavaScript calls causing style recalculation and layout.

## Google Earth for Web beta available

[Jordon Mears](https://web.dev/earth-webassembly)‎: The preview version of Google Earth for Web powered by WebAssembly is now available. You can try it out ([direct link](https://earth.google.com/web/?beta=1)) in Chromium-based browsers and Firefox — it runs single-threaded in browsers that don’t have yet (re-)enabled SharedArrayBuffer — but not in Safari because of its lack of full support for WebGL2.

![](/media/google-earth-web.png)

## Browsers can keep session cookies alive

[Eric Lawrence](https://textslashplain.com/2019/06/24/surprise-undead-session-cookies/): Chrome and Firefox allow users to restore the previous browser session on startup. With this option enabled, closing the browser will not delete the user’s session cookies nor empty the `sessionStorage` of web pages.

> Given this session resumption behavior, it’s more important than ever to ensure that your site behaves reasonably upon receipt of an outdated session cookie (e.g., redirect the user to the login page instead of showing an error).

## SVG geometry properties in CSS

[Jérémie Patonnier](https://mobile.twitter.com/JeremiePat/status/1143095982651072512): Firefox Nightly has implemented SVG’s geometry properties (`x`, `y`, `r`, etc.) in CSS. This feature is already supported in Chrome and Safari, and is expected to ship in Firefox 69 (in September).

https://codepen.io/simevidas/pen/WqEXdw?editors=1100
