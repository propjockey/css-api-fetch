[![Jane Ori - PropJockey.io](https://img.shields.io/badge/Jane%20Ori%20%F0%9F%91%BD-%F0%9F%A4%8D%20PropJockey.io-7300E6.svg?labelColor=FB04C2&style=plastic)](http://jane.propjockey.io/)

# css-api-fetch from <img src="https://github.com/user-attachments/assets/87119fb5-c39d-429a-9bfd-424f0e100720" alt="" width="30px"> PropJockey
Make remote API Requests in CSS (Cascading Style Sheets) and store the response data in `--vars` on `:root` *without JavaScript*.


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

See `./html-templates.md` for instructions.

### Customize API endpoints in the CSS

You can save responses to `:root` from up to 4 different API requests.

`api-id-1` `api-id-2` `api-id-3` `api-id-4`

You can specify the corresponding endpoints in your CSS:

```css
@container style(--api-id: 1) {
  .api-fetch { --api-fetch: url(https://css-api.propjockey.io/os-country.php); }
}
@container style(--api-id: 2) {
  .api-fetch { --api-fetch: url(https://picsum.photos/512/256); }
}
...
```

you can add any other CSS conditions you desire, `--api-id` is the only requirement. You can also use any number of urls for a single api id but the response data will be overwritten if you send a second request to the same api-id.

## Setting up a compatible API

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
https://codepen.io/propjockey/pen/pvzrWyG/f753d87ebc1dd25fb6f5d674698fb7a0?editors=1100

## Accessing the remote request's Response Data

Once a request is complete, the following set of 10 variables will be set on `:root` for each api id. They are all 0 prior to any corresponding requests.

```css
@property --api-1-response-0 { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-1-response-1 { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-1-response-2 { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-1-response-3 { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-1-response-4 { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-1-response-5 { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-1-response-6 { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-1-response-7 { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-1-response-8 { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-1-response-9 { syntax: "<integer>"; inherits: true; initial-value: 0; }
...
@property --api-2-response-0 { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-2-response-1 { syntax: "<integer>"; inherits: true; initial-value: 0; }
...
```

the response variables hold each decimal digit of the width followed by each of the height. You can use `calc()` and other techniques to do any decoding necessary. Please reach out if you have a specific goal, there's not much that can't be done yet.

For example, [css-bin-bits](https://propjockey.github.io/css-bin-bits/) can help you convert 16 bit decimal numbers between decimal and binary and perform bitwise operations on the values without JS.

An image returned from `api-id-3` that's `129px` wide and `65535px` tall would have the data:

```css
--api-3-response-0: 0;
--api-3-response-1: 0;
--api-3-response-2: 1;
--api-3-response-3: 2;
--api-3-response-4: 9;
--api-3-response-5: 6;
--api-3-response-6: 5;
--api-3-response-7: 5;
--api-3-response-8: 3;
--api-3-response-9: 5;
```

Additionally, there are 2 status bits available for all 4 api ids:

```css
@property --api-1-in-progress { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-1-complete { syntax: "<integer>"; inherits: true; initial-value: 0; }

@property --api-2-in-progress { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-2-complete { syntax: "<integer>"; inherits: true; initial-value: 0; }

@property --api-3-in-progress { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-3-complete { syntax: "<integer>"; inherits: true; initial-value: 0; }

@property --api-4-in-progress { syntax: "<integer>"; inherits: true; initial-value: 0; }
@property --api-4-complete { syntax: "<integer>"; inherits: true; initial-value: 0; }
```

they will both be 0 before any corresponding api requests have been triggered.

## Open Contact 👽

Please do reach out if you need help with any of this, have feature requests, want to share what you've created, or wish to learn more.

| PropJockey.io | CodePen | DEV Blog | GitHub | Mastodon |
| --- | --- | --- | --- | --- |
| [![PropJockey.io](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/propjockey-lines.svg)](https://propjockey.io) | [![CodePen](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/codepen.svg)](https://codepen.io/propjockey) | [![DEV Blog](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/dev.svg)](https://dev.to/janeori) | [![GitHub](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/github.svg)](https://github.com/propjockey) | [![Mastodon](https://raw.githubusercontent.com/propjockey/propjockey-brand/main/external-social/100px/mastodon.svg)](https://front-end.social/@JaneOri) |


[🦋@JaneOri.PropJockey.io](https://bsky.app/profile/janeori.propjockey.io)

[𝕏@Jane0ri](https://x.com/jane0ri)
