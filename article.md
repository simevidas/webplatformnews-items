# Weekly platform news: Tracking via web storage, First Input Delay, navigating headings

## Safari’s tracking prevention limits web storage

Some social networks and other websites that engage in cross-site tracking add a query string or fragment to external links for tracking purposes (Apple calls this “abuse of link decoration”).

When people navigate from websites with tracking abilities to other websites via such “decorated” links, Safari will expire the cookies that are created on the loaded web pages after 24 hours. This has led some trackers to start using other types of storage (e.g., `localStorage`) to track people on websites.

As a new countermeasure, Safari will now delete _all non-cookie website data_ in these scenarios if the user hasn’t interacted with the website for seven days.

> The reason why we cap the lifetime of script-writable storage is simple. Site owners have been convinced to deploy third-party scripts on their websites for years. Now those scripts are being repurposed to circumvent browsers’ protections against third-party tracking. By limiting the ability to use any script-writable storage for cross-site tracking purposes, [Safari’s tracking prevention] makes sure that third-party scripts cannot leverage the storage powers they have gained over all these websites.

<small>(via [John Wilander](https://webkit.org/blog/9521/intelligent-tracking-prevention-2-3/))</small>

## First Input Delay is much worse on mobile

First Input Delay (FID), the [delay until the page is able to respond to the user](https://youtu.be/ymxs8OSXiUA?t=167), is much worse on mobile: Only 13% of websites have a fast FID on mobile, compared to 70% on desktop.

![](/media/fid-desktop-mobile.jpg)

Tip: If your website is popular enough to be included in the Chrome UX Report, you can check your site’s mobile vs. desktop FID data on [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/).

<small>(via [Rick Viscomi](https://twitter.com/rick_viscomi/status/1176731125991038978))</small>

## Screen reader users navigate web pages by headings

According to WebAIM’s recent screen reader user survey, the most popular screen readers are NVDA (41%) and JAWS (40%) on desktop, and VoiceOver (71%) and TalkBack (33%) on mobile.

When trying to find information on a web page, most screen reader users navigate the page through the headings (`<h1>`, `<h2>`, `<h3>`, etc.).

> The usefulness of proper heading structures is very high, with 86.1% of respondents finding heading levels very or somewhat useful.

Tip: You can check a web page’s heading structure with W3C’s [Nu Html Checker](https://validator.w3.org/nu/) (enable the “outline” option).

![](/media/heading-level-outline.png)

<small>(via [WebAIM](https://twitter.com/webaim/status/1178383652658397184))</small>

## More news…

![](/media/sunday-issue-11.png)

Read even more news in my weekly **Sunday issue** that can be delivered to you via email every Monday morning.

[Web Platform News: Sunday issue →](https://webplatform.news/issues/2019-08-30)
