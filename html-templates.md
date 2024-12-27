# HTML templating for css-api setup and usage

The html in each part should be used exactly as-is.

The html comments can be replaced as defined lower in this document.

Nothing else should change and it should all be included, including the outer `css-api` wrapper.

## Primary interface

Ideally this will be placed right before the close `</body>` tag to minimize interference with functionality.

```html
<div class="css-api">
  <div class="api-debug-off"></div>

  <!-- api-trigger api-once api-id-1 -->
  <!-- api-trigger api-once api-id-2 -->
  <!-- api-trigger api-once api-id-3 -->
  <!-- api-trigger api-once api-id-4 -->

  <div class="api-fetch">
    <div class="api-parse">
      <div class="api-response">
        <div class="api-handler">
          <ol class="api-transfer-value-0 api-cpu">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-value-1 api-cpu">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-value-2 api-cpu">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-value-3 api-cpu">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-value-4 api-cpu">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-value-5 api-cpu">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-value-6 api-cpu">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-value-7 api-cpu">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-value-8 api-cpu">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-value-9 api-cpu">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-complete api-cpu api-id-1">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-complete api-cpu api-id-2">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-complete api-cpu api-id-3">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
          <ol class="api-transfer-complete api-cpu api-id-4">
            <li class="api-cpu-phase-0"></li>
            <li class="api-cpu-phase-1"></li>
            <li class="api-cpu-phase-2"></li>
            <li class="api-cpu-phase-3"></li>
          </ol>
        </div>
      </div>
    </div>
  </div>
</div>
```

## `<!-- api-trigger api-once api-id-1 -->`

Trigger elements fire off the remote API Request corresponding to `api-id-1` when you `:hover` them.

```html
  <div class="api-trigger api-once api-id-1">
    <!-- api-messages -->
    <ol class="api-cpu">
      <li class="api-cpu-phase-0"></li>
      <li class="api-cpu-phase-1"></li>
      <li class="api-cpu-phase-2"></li>
      <li class="api-cpu-phase-3"></li>
    </ol>
  </div>
```

Optionally, if the element is a button, it will not trigger until it has `:focus` by click or tab.

```html
  <button class="api-trigger api-once api-id-1">
    <!-- api-messages -->
    <ol class="api-cpu">
      <li class="api-cpu-phase-0"></li>
      <li class="api-cpu-phase-1"></li>
      <li class="api-cpu-phase-2"></li>
      <li class="api-cpu-phase-3"></li>
    </ol>
  </button>
```

Add a your own additional class name to the outer `api-trigger` element to position it anywhere you want. Fixed, absolute, anchor, etc.

If you wish to maximize chances of success, do not modify the positioning, transform, or z-index of any other elements provided here. Only the `api-trigger` elements are designed to be positioned with custom CSS.

You can remove `api-once` from the `api-trigger` element if you wish for the API to be requested every time the trigger is interacted with.

### `<!-- api-trigger api-once api-id-2 -->`

The same as `api-id-1` but for `api-id-2`, set by the class name of the outer element.

### `<!-- api-trigger api-once api-id-3 -->`

The same as `api-id-1` but for `api-id-3`, set by the class name of the outer element.

### `<!-- api-trigger api-once api-id-4 -->`

The same as `api-id-1` but for `api-id-4`, set by the class name of the outer element.

## `<!-- api-messages -->`

Can be anything you want. Text, images, elements.

If you want specific, status aware messages, use this html specifically and replace the innerHTML of each `<li>` with anything you want. Text, images, elements.

```html
  <ol class="api-messages">
    <li class="api-prompt"><!-- prompt to initiate the request --></li>
    <li class="api-in-progress"><!-- displayed while in progress --></li>
    <li class="api-continue"><!-- shown when in progress but the screen isn't :hover'd (:hover required) --></li>
    <li class="api-complete"><!-- shown when complete and the response data is available --></li>
  </ol>
```

If your designs for the elements here interferes with `css-api` functionality, consider making your content:

`pointer-events: none;`

## Open Contact 👽

PLEASE reach out if you need help with any of this, have feature requests, or wish to learn more.

| PropJockey.io | CodePen | DEV Blog | GitHub | Mastodon |
| --- | --- | --- | --- | --- |
| [![PropJockey.io](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/propjockey-lines.svg)](https://propjockey.io) | [![CodePen](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/codepen.svg)](https://codepen.io/propjockey) | [![DEV Blog](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/dev.svg)](https://dev.to/janeori) | [![GitHub](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/github.svg)](https://github.com/propjockey) | [![Mastodon](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/mastodon.svg)](https://front-end.social/@JaneOri) |


[🦋@JaneOri.PropJockey.io](https://bsky.app/profile/janeori.propjockey.io)

[𝕏@Jane0ri](https://x.com/jane0ri)
