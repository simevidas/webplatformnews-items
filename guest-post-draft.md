# Weekly news: Mozilla’s AV1 encoder, Samsung One UI CSS, DOM `matches` method

`<EDITOR_INTRO>`  
Šime posts regular content for web developers on [webplatform.news](https://webplatform.news).  
`</EDITOR_INTRO>`

## Vimeo partners with Mozilla to use their rav1e encoder

[Vittorio Giovara](https://medium.com/vimeo-engineering-blog/behind-the-scenes-of-av1-at-vimeo-a2115973314b): AV1 is a royalty-free video codec designed by the Alliance for Open Media and the the most anticipated successor of H.264. Vimeo is contributing to the development of Mozilla’s AV1 encoder.

> In order for AV1 to succeed, there is a need of an encoder like x264, a free and open-source encoder, written by the community, for the community, and available to everyone: rav1e. Vimeo believes in what Mozilla is doing.

## Use the `aria-describedby` attribute to bind instructions to form fields

[Raghavendra Satish Peri](https://www.deque.com/blog/anatomy-of-accessible-forms-best-practices/): If you provide additional instructions for a form field, use the `aria-describedby` attribute to bind the instruction to the field. Otherwise, assistive technology users who use the Tab key might miss this information.

```html
<label for="dob">Date of Birth</label>
<input type="text" aria-describedby="dob1" id="dob" />
<span id="dob1">Use DD/MM/YY</span>
```

## Samsung Internet announces One UI CSS

[Diego González](https://medium.com/samsung-internet-dev/one-ui-to-rule-them-all-f2b26e283b48): Samsung is experimentally developing a CSS library based on its new One UI design language. The library is called One UI CSS and includes styles for common form controls such as buttons, menus, and sliders, as well as other assets (web fonts, SVG icons, polyfills).

![Some of the controls present in One UI CSS](/media/one-ui-css.png)

## DOM elements have a `matches` method

[Sam Thorogood](https://dev.to/samthor/matching-elements-with-selectors-in-js-4991): You can use the `matches` method to test if a DOM element has a specific CSS class, attribute or ID value. This method accepts a CSS selector and returns `true` if the element matches the given selector.

```js
el.classList.has('foo')  /* becomes */ el.matches('.foo');
el.hasAttribute('hello') /* becomes */ el.matches('[hello]');
el.id === 'bar'          /* becomes */ el.matches('#bar');
```
