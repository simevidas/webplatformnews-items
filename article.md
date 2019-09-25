# Weekly platform news: Checking your site for layout shifts, high-bitrate videos are more likely to stall, Firefox’s command for capturing screenshots

## Identifying the causes of layout shifts during page load

You can now use WebPageTest to capture any layout shifts that occur on your website during page load, and identify what caused them.

1. On [webpagetest.org](https://www.webpagetest.org/), paste the following snippet into the “Custom Metrics” field in the _Custom_ tab (under _Advanced Settings_) and make sure that a Chrome browser is selected.

   <!-- prettier-ignore -->
   ```javascript
   [LayoutShifts]
   return new Promise(resolve => {
     new PerformanceObserver(list => {
       resolve(JSON.stringify(list.getEntries().filter(entry => !entry.hadRecentInput)));
     }).observe({type: "layout-shift", buffered: true});
   });
   ```

1. After completing the test, inspect the captured `LayoutShifts` entries on the _Custom Metrics_ page, which is linked from the _Details_ section.

   ![](/media/webpagetest-custom-metrics.jpg)

1. Based on the `"startTime"` and `"value"` numbers in the data, use WebPageTest’s filmstrip view to pinpoint the individual layout shifts and identify their causes.

<small>(via [Rick Viscomi](https://dev.to/chromiumdev/fixing-layout-instability-176c))</small>

## A high bitrate can cause your videos to stall

If you serve videos for your website from your own web server, keep an eye on the video bitrate (the author suggests FFmpeg and [streamclarity.com](https://twitter.com/dougsillars/status/1175818330596360194)). If your video has a bitrate of over 1.5 Mbps, playback may stall one or more times for people on 3G connections, depending on the video’s length.

> 50% of videos in this study have a bitrate that is greater than the downlink speed of a 3G connection — meaning that video playback will be delayed and contain stalls.

![](/media/video-stall-data.png)

<small>(via [Doug Sillars](https://twitter.com/dougsillars/status/1173571080155516928))</small>

## Firefox’s `:screenshot` command

Firefox’s DevTools console includes a powerful command for capturing screenshots of the current web page. Like in Chrome DevTools, you can capture a screenshot of an individual element, the current viewport, or the full page, but Firefox’s `:screenshot` command also provides advanced options for adjusting the device pixel ratio and setting a delay.

```
// capture a full-page screenshot at a device pixel ratio of 2
:screenshot --fullpage --dpr 2

// capture a screenshot of the viewport with a 5-second delay
:screenshot --delay 5
```

<small>(via [Reddit](https://www.reddit.com/r/firefox/comments/d7zelb/til_how_to_take_a_high_dpi_website_screenshot_in/))</small>

---

Read even more news in my weekly **Sunday issue**, which can be delivered to you via email every Monday morning.

![](/media/sunday-issue-10.png)

[Web Platform News: Sunday issue →](https://webplatform.news/issues/2019-08-30)
