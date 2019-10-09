# Weekly platform news: Impact of Third-Party Code, Passive Mixed Content, Countries with the Slowest Connections

## Measure the impact of third-party code during page load

Lighthouse, Chrome’s built-in auditing tool, now shows a warning when the impact of third-party code on page load performance is too high. The pre-existing “Third-party usage” diagnostic audit will now _fail_ if the total main-thread blocking time caused by third-parties is larger than 250 ms during page load.

![](/media/impact-third-party-code.png)

Note: This feature was added in Lighthouse version 5.3.0, which is currently available in Chrome Canary.

<small>(via [Patrick Hulce](https://github.com/googlechrome/lighthouse/pull/9486))</small>

## Passive mixed content is coming to an end

Currently, browsers still allow web pages loaded over a secure connection (HTTPS) to load images, videos, and audio over an insecure connection. Such insecurely-loaded resources on securely-loaded pages are known as “passive mixed content,” and they represent a [security and privacy risk](https://w3c.github.io/webappsec-mixed-content/level2.html#intro).

> An insecurely-loaded image can allow an attacker to communicate incorrect information to the user (e.g., a fabricated stock chart), mutate client-side state (e.g., set a cookie), or induce the user to take an unintended action (e.g., changing the label on a button).

Starting next February, Chrome will auto-upgrade all passive mixed content to `https:`, and resources that fail to load over `https:` will be blocked. According to data from Chrome Beta, auto-upgrade currently fails for about 30% of image loads.

<small>(via [Emily Stark](https://twitter.com/estark37/status/1179812991862112256))</small>

## Fast connections are still not common in many countries

Data from Chrome UX Report shows that there are still many countries and territories in the world where most people access the Internet over a 3G or slower connection. (This includes a number of small island nations that are not visible on this map.)

![](/media/countries-slow-connections.png)

<small>(via [Paul Calvano](https://twitter.com/paulcalvano/status/1179811059835822080))</small>

## More news…

![](/media/sunday-issue-12.png)

Read even more news in my weekly **Sunday issue** that can be delivered to you via email every Monday morning.

<a href="https://webplatform.news/issues/2019-08-30" class="button">More News →</a>
