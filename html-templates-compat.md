# HTML templating for css-api-fetch setup and usage

The html should be used exactly as-is unless noted otherwise.

The html comment can be replaced with any presentation you want.

```html
<div class="css-api-fetch-compat api-debug-compat-off">
  <div class="api-fetch-compat">
    <div class="api-parse-compat">
      <div class="api-response-compat">
        <!-- your presentation here -->
      </div>
    </div>
  </div>
</div>
```

Adding a class name or style attribute to the outer `.css-api-fetch-compat` element is fine.

On that outer element, set the following variables:

```css
.my-class-name.css-api-fetch-compat {
  --api-height: 100px;
  --api-width: 100px;
  --api-fetch: url(https://picsum.photos/512/256);
}
```
These variables can be set higher up in DOM if that is convinient, this wrapper will inherit them.

You may also set `position` and the `inset` properties. Do not modify `width` or `height` directly. Avoid setting any other properties.

CSS's viewport units are fine to use here.

Avoid modifying any CSS for `.api-fetch-compat`, `.api-parse-compat`, or `.api-response-compat`.

Your presentation can contain any elements and styling you wish.

The response data will be available to your presentation's content in these two variables:

`var(--api-w)` and `var(--api-h)`

Each will be a value between 0 and 99,999 which is just over 16 bits.

There is also a single bit flag indicating if the response has been recieved: `var(--api-ready)`.

Demo:

https://codepen.io/propjockey/pen/EaYvdey

## Open Contact 👽

Please do reach out if you need help with any of this, have feature requests, want to share what you've created, or wish to learn more.

| PropJockey.io | CodePen | DEV Blog | GitHub | Mastodon |
| --- | --- | --- | --- | --- |
| [![PropJockey.io](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/propjockey-lines.svg)](https://propjockey.io) | [![CodePen](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/codepen.svg)](https://codepen.io/propjockey) | [![DEV Blog](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/dev.svg)](https://dev.to/janeori) | [![GitHub](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/github.svg)](https://github.com/propjockey) | [![Mastodon](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/mastodon.svg)](https://front-end.social/@JaneOri) |


[🦋@JaneOri.PropJockey.io](https://bsky.app/profile/janeori.propjockey.io)

[𝕏@Jane0ri](https://x.com/jane0ri)
