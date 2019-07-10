# Weekly news: HTML inspection in Search Console, global scope of scripts, Babel `env` adds `defaults` query

## Easier HTML inspection in Google Search Console

[Barry Schwartz](https://searchengineland.com/google-search-console-adds-search-within-markup-copy-with-tweaking-318676): The URL Inspection tool in Google Search Console now includes useful controls for searching within and copying the HTML code of the crawled page.

![](/media/google-search-console-html.png)

**Note:** The URL Inspection tool provides information about Google’s indexed version of a specific page. You can access Google Search Console at https://search.google.com/search-console.

## CSS properties are computed once per element

[Miriam Suzanne](https://www.smashingmagazine.com/2019/07/css-custom-properties-cascade/#inherited-versus-universal): The value of a CSS custom property is computed once per element. If you define on the `<html>` element a custom property `--func` that uses the value of another custom property `--val`, then re-defining the value of `--val` on a nested DOM element that uses `--func` won’t have any effect because the inherited value of `--func` is already computed.

```css
html {
  --angle: 90deg;
  --gradient: linear-gradient(var(--angle), blue, red);
}

header {
  --angle: 270deg; /* ignored */
  background-image: var(--gradient); /* inherited value */
}
```

## The global scope of scripts

[Surma](https://mobile.twitter.com/DasSurma/status/1145990244069707776): JavaScript variables created via `let`, `const`, or `class` declarations at the top level of a script (`<script>` element) continue to be defined in subsequent scripts of the page. (Ed. note: Axel Rauschmayer calls this the “[global scope of scripts](https://mobile.twitter.com/rauschma/status/1145994986057535488).”)

![](/media/global-scope-of-scripts.png)

## Babel `env` now supports the `defaults` query

[Nicolò Ribaudo](https://babeljs.io/blog/2019/07/03/7.5.0.html): Babel’s `env` preset ([@babel/preset-env](https://babeljs.io/docs/en/babel-preset-env)) now allows you to target Browserslist’s default browsers (see the full list at [browsersl.ist](https://browsersl.ist/)). Note that if you don’t specify your target browsers, Babel `env` will run _every_ syntax transform on your code.

```json
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "targets": { "browsers": "defaults" }
      }
    ]
  ]
}
```

## All news items from June 2019 [PDF]

For your convenience, I have compiled all 59 news items that I’ve published throughout June into one 10-page PDF document: **[Download it here](/media/web-platform-news-june-2019.pdf)**.

![](/media/web-platform-news-june-2019.png)
