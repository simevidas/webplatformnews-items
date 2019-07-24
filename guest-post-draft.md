# Weekly news: Truncating muti-line text, `calc()` in custom property values, Contextual Alternates

## Truncating mutli-line text

The CSS `-webkit-line-clamp` property for truncating multi-line text is now widely supported (see my [usage guide](https://webplatform.news/issues/2019-05-17)). If you use **Autoprefixer**, update it to the latest version (9.6.1). Previous versions would remove `-webkit-box-orient: vertical`, which caused this CSS feature to stop working.

**Note:** Autoprefixer doesn’t generate any prefixes for you in this case. You need to use the following four declarations exactly (all are required):

```css
.line-clamp {
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3; /* or any other integer */
}
```

**Source:** [Autoprefixer’s post on Twitter](https://mobile.twitter.com/Autoprefixer/status/1147505748261396480)

## Calculations in CSS custom property values

In CSS it is currently not possible to pre-calculate custom property values. The computed value of a custom property is its specified value (with variables substituted); therefore, relative values in `calc()` expressions are _not_ “absolutized” (e.g., `em` values are not computed to `px` values).

![](/media/css-custom-properties.png)

**Spec:** https://drafts.csswg.org/css-variables/#defining-variables

```css
:root {
  --large: calc(1em + 10px);
}

blockquote {
  font-size: var(--large);
}
```

In the above example, it may appear that the calculation is performed on the root element, specifically that the relative value `1em` is computed and added to the absolute value `10px`. Under default conditions (`1em` = `16px` on the root element), the computed value of `--large` would be `26px`.

But that’s not what’s happening here. The computed value of `--large` is its specified value, `calc(1em + 10px)`. This value is inherited and substituted into the value of the `font-size` property on the `<blockquote>` element.

```css
blockquote {
  /* the declaration after variable substitution */
  font-size: calc(1em + 10px);
}
```

Finally, the calculation is performed and the relative `1em` value absolutized in the scope of the `<blockquote>` element — _not_ the root element where the `calc()` expression is declared.

**Source:** [Tab Atkins Jr.’s reply on Twitter](https://mobile.twitter.com/tabatkins/status/1153515846670512128)

## Contextual Alternates

The “Contextual Alternates” OpenType feature ensures that characters don’t overlap or collide when ligatures are turned off. You can check if your font supports this feature on [wakamaifondue.com](https://wakamaifondue.com/) and enable it (if necessary) via the CSS `font-variant-ligatures: contextual` declaration.

![](/media/contextual-alternates.png)

**Source:** “[Contextual Alternations (for a fraction of the price)](https://rwt.io/typography-tips/contextual-alternations-fraction-price)” by Jason Pamental

## Announcing daily news on webplatform.news

Announcement: I have started posting daily news for web developers on [webplatform.news](https://webplatform.news). Visit every day!

![](/media/web-platform-daily-vs-news.png)
