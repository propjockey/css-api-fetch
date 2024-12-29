[![Jane Ori - PropJockey.io](https://img.shields.io/badge/Jane%20Ori%20%F0%9F%91%BD-%F0%9F%A4%8D%20PropJockey.io-7300E6.svg?labelColor=FB04C2&style=plastic)](http://jane.propjockey.io/)

# css-api-fetch from <img src="https://github.com/user-attachments/assets/87119fb5-c39d-429a-9bfd-424f0e100720" alt="" width="30px"> PropJockey
Make remote API Requests in CSS (Cascading Style Sheets) and store the response data in `--vars` on `:root` *without JavaScript*.

## api-fetch.css, api-fetch-root.css, or api-fetch-compat.css?

There are 3 css files you can use with different trade-offs.

1) `api-fetch.css` - contains both of the following

2) `api-fetch-root.css`

* currently only works in Chrome
* Response data is lifted to `:root` and can be used anywhere.
* Up to 4 responses can be stored at the same time for use anywhere in your project.
* Triggering the request requires specific setup but there are no limits on when you choose to initiate the requests.

3) `api-fetch-compat.css`

* works in Chrome, FireFox, Safari
* Does not lift the response data to `:root`, it can only be used within the element.
* Does not let you store more than one response at a time unless they are in sepearate elements.
* The element that contains the response data must have a fixed width and height and can't automatically resize based on the content.
* Overflow is hidden and can't be avoided.
* Anything you build that uses the single response must be within the provided element.
* Triggering the request is in your hands, based on however/whenever you choose to set the `url()`

## Installation and Setup

`css-api-fetch` requires specific html in additon to the CSS.

### Add the CSS first:

`$ npm install css-api-fetch`

Then include `/node_modules/css-api-fetch/api-fetch.css`

#### OR Use your favorite NPM CDN for small projects

From html:

```html
<link rel="stylesheet" type="text/css" href="https://unpkg.com/css-api-fetch@1/api-fetch.css">
```

or directly from your CSS:

```css
@import url(https://unpkg.com/css-api-fetch@1/api-fetch.css);
```

### Adding the HTML

See `./html-templates-compat.md` for instructions on the `compat` version setup and usage.

For the `root` version, add a single tag anywhere on the page per api you want to use:

```html
<div class="api-fetch-1"></div>
```

You can save responses to `:root` from up to 4 different API requests at the same time.

`api-fetch-1` `api-fetch-2` `api-fetch-3` `api-fetch-4`

Use separate html elements for each of these, do not nest anything inside.

If you wish to see debug info, add this tag anywhere on the page:

```html
<div class="api-debug-on"></div>
```

Both versions, `root` and `compat`, can be used at the same time.

### Customize API endpoints in the CSS (:root version)

You can specify any of the API endpoints anywhere in your CSS so long as the var is visible to the corresponding `api-fetch-X` tag:

```css
body {
  --api-fetch-1: url(https://css-api.propjockey.io/os-country.php);
  --api-fetch-2: url(https://picsum.photos/512/256);
  --api-fetch-3: url(https://picsum.photos/100/222);
  --api-fetch-4: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="0px" height="99999px"></svg>');
}
```

You may want to only fetch this API data in specific app state conditions.

You can easily use container style queries to conditionally use an endpoint:

```css
@container style(--amazing-computation: 0) {
  .api-fetch-2 { --api-fetch-2: none; }
}
@container style(--amazing-computation: 1) {
  .api-fetch-2 { --api-fetch-2: url(...) }
}
...
```

## Setting up a compatible API (both versions)

`css-api-fetch` expects an image response with the response data encoded into the height and width.

The maximum width is `99999px` which is more than 16 bits of data.

The maximum height is also `99999px` which is more than 32 bits of data total.

### For example, getting the user's IP Address with CSS

Here, is php generating an svg that encodes the 32 bit request IP Address:

```php
<?php
  header('Content-type: image/svg+xml');

  $adr = $_SERVER['REMOTE_ADDR'] ?: '255.255.255.255';
  $hex = str_pad(implode(array_map('dechex', explode('.', $adr, 4))), 8, '0', STR_PAD_LEFT);
  $width = hexdec(preg_replace('/(^0{0,3})|(.{4}$)/', '', $hex) ?: '0');
  $height = hexdec(preg_replace('/^.{4}0{0,3}/', '', $hex) ?: '0');

  echo '<svg xmlns="http://www.w3.org/2000/svg" width="' . $width . 'px" height="' . $height . 'px"></svg>';
?>
```

16 bits in width, 16 bits in height

Here is a live example of this in action:

[![screenshot of the live demo here](https://github.com/user-attachments/assets/2248a215-cb69-4708-860c-cd1b644f6422)](https://codepen.io/propjockey/pen/JoPyxrK/a2aec757b3cd020a7e1bddce17ff31ed?editors=1100)


## Accessing the remote request's Response Data (:root version)

Once a request is complete, response data from the width and height of the image will be returned and set on root as an integer.

```css
@property --api-1-w { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-1-h { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-2-w { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-2-h { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-3-w { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-3-h { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-4-w { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-4-h { syntax: "<integer>"; inherits: true; initial-value: 0; }
```

You can use `calc()` and other techniques to do any decoding necessary. Please reach out if you have a specific goal, there's not much that can't be done yet.

For example, [css-bin-bits](https://propjockey.github.io/css-bin-bits/) can help you convert 16 bit decimal numbers between decimal and binary and perform bitwise operations on the values without JS.

Additionally, there is a ready bit available for all 4 api ids that will be set to `1` when it has any non-0 data:

```css
@property --api-1-ready { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-2-ready { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-3-ready { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-4-ready { syntax: "<integer>"; inherits: true; initial-value: 0; }
```

## Open Contact 👽

Please do reach out if you need help with any of this, have feature requests, want to share what you've created, or wish to learn more.

| PropJockey.io | CodePen | DEV Blog | GitHub | Mastodon |
| --- | --- | --- | --- | --- |
| [![PropJockey.io](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/propjockey-lines.svg)](https://propjockey.io) | [![CodePen](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/codepen.svg)](https://codepen.io/propjockey) | [![DEV Blog](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/dev.svg)](https://dev.to/janeori) | [![GitHub](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/github.svg)](https://github.com/propjockey) | [![Mastodon](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/mastodon.svg)](https://front-end.social/@JaneOri) |


[🦋@JaneOri.PropJockey.io](https://bsky.app/profile/janeori.propjockey.io)

[𝕏@Jane0ri](https://x.com/jane0ri)
