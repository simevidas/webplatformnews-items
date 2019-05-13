# Weekly news: 

`<EDITOR_INTRO>`  
Šime posts regular content for web developers on [webplatform.news](https://webplatform.news).  
`</EDITOR_INTRO>`

## Installed PWAs on iOS cannot easily be restarted

[Maximiliano Firtman](https://mobile.twitter.com/firt/status/1110649483614961669): On iOS, it is not possible to restart an installed PWA by closing it from the [_recently used apps_ screen](https://support.apple.com/en-us/HT201330) and then immediately reopening it. Instead of restarting the app, iOS restores its state. This can be a problem for users if the PWA gets stuck in a broken state ([example](https://mobile.twitter.com/croozeus/status/1116194635242598400)).

> After some undefined time, the saved context seems to disappear. So if you get out of the PWA, do nothing with your phone and wait some hours to go back to the PWA, it restarts from scratch.

![](/media/ios-pwa-restart.png)

## Instilling a performance culcure at The Telegraph

[Gareth Clubb](https://mobile.twitter.com/digitalclubb/status/1123245409953034240): At The Telegraph (a major UK newspaper), we set up a web performance working group to tackle our “organizational” performance challenges and instill a performance culture. The group meets regularly to review third-party tags and work on improving our site’s performance.

We’ve started deferring all JavaScript (including our own) using the `<script defer>` attribute. This change alone nearly doubled our (unthrottled) Lighthouse performance score.

> Deferring our JavaScript hasn’t skewed any existing analytics and it certainly hasn’t delayed any advertising. … The First Ad Loaded metric improved by an average of four seconds.

We also removed 1 MB of third-party payload from our new front end. When one of our teams requests the addition of any new script, we now test the script in isolation and reject it if it degrades our metrics (first contentful paint, etc.).

> When we started this process, we had a collection of very old scripts and couldn’t track the original requester. We removed those on the premise that, if they were important, people would get back in touch — no one did.
  
## Microsoft plans to add tracking prevention to the Edge browser

[Kyle Pflug](https://blogs.windows.com/msedgedev/2019/05/06/edge-chromium-build-2019-pwa-ie-mode-devtools/): Microsoft has announced plans to add options for <mark>blocking trackers</mark> to the Edge browser. Malicious trackers would be blocked automatically, and the user would have the option to additionally block _all_ potential trackers.

![](/media/edge-tracking-prevention.jpg)

**Note:** This would make Edge the _fourth_ major browser with some form of built-in anti-tracking feature (two other major browsers, Opera and UC Browser, include ad blockers instead).

1. In 2015, Firefox added [Tracking Protection](https://blog.mozilla.org/futurereleases/2015/09/23/help-test-private-browsing-with-tracking-protection-in-firefox-beta/) — recently renamed to Content Blocking — becoming the first major browser to protect users from third-party trackers (when browsing the web in private mode).

1. Since 2017, Safari prevents cross-site tracking by default, through a feature called [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) (ITP). Users are prompted to allow tracking when they try to interact with third-party widgets on websites.

   ![](/media/safari-tracking-prompt.png)

1. Earlier this year, Samsung Internet added an experimental feature called [Smart Anti-Tracking](https://medium.com/samsung-internet-dev/new-year-new-samsung-internet-b74f282e4429) that denies third-party trackers access to cookies.
