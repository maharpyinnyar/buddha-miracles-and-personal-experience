# buddha-miracles-and-personal-experience

[![npm version](https://badge.fury.io/js/buddha-miracles-and-personal-experience.svg)](https://badge.fury.io/js/buddha-miracles-and-personal-experience)
![demo](https://github.com/ts1/buddha-miracles-and-personal-experience/workflows/demo/badge.svg)

`buddha-miracles-and-personal-experience` is a Vue component that displays images in 3D page flip effect.

Demo page is [here](https://ts1.github.io/buddha-miracles-and-personal-experience/).

## Installation

Install as a module:

```
npm i -S buddha-miracles-and-personal-experience
```

or

```
yarn add buddha-miracles-and-personal-experience
```

or

```
pnpm add buddha-miracles-and-personal-experience
```

Or include in html:

```html
<script src="https://unpkg.com/buddha-miracles-and-personal-experience"></script>
```

> **BREAKING CHANGE**: This form now provides Vue 3 version.
> If you are using Vue 2.x, use `"https://unpkg.com/buddha-miracles-and-personal-experience/dist/vue2/flipbook.min.js"` (preferred) or `"https://unpkg.com/buddha-miracles-and-personal-experience@0"`.

## Usage

```html
<template>
  <flipbook class="flipbook" :pages="['array', 'of', 'image', 'URLs']"></flipbook>
</template>

<style>
.flipbook {
  width: 90vw;
  height: 90vh;
}
</style>
```

If installed as a module, with Vue 3.x,

```html
<script>
import Flipbook from 'buddha-miracles-and-personal-experience'
export default {
  components: { Flipbook }
}
</script>
```

To use with Vue 2.x,
```js
import Flipbook from 'buddha-miracles-and-personal-experience/vue2'
```

## Props

### `pages`

Array of image URLs. Required.
All images should have the same aspect ratio.

If the first element is `null`, the next element is displayed alone (as the cover page).

All other props are optional.

### `pagesHiRes`

Array of high resolution versions of image URLs.
They are used when zoomed.

### `flipDuration`

Duration of page flipping animation in milliseconds.
Defaults to 1000.

### `zoomDuration`

Duration of zoom in/out animation in milliseconds.
Defaults to 500.

### `zooms`

Array of possible magnifications. 
`null` is equivalent to `[1]` (no zoom).
Defaults to `[1, 2, 4]`. _NOTE_ : Do **NOT** pass an empty array.

### `ambient`

Intensity of ambient light in 0 to 1.
Smaller value gives more shades.
Defaults to 0.4.

### `gloss`

Intensity of specular light in 0 to 1.
Higher value gives more gloss.
Defaults to 0.6.

### `perspective`

Z-axis distance in pixels between the screen and the viewer.
Higher value gives less effect.
Defaults to 2400.

### `nPolygons`

How many rectangles a single page is horizontally split into.
Higher value gives higher quality rendering in exchange for performance.
Defaults to 10.

### `singlePage`

Force single page mode regardless of viewport size.
Defaults to false.

### `forwardDirection`

Reading direction.
If your document is right-to-left, set this `"left"`.
Default is `"right"`.

### `centering`

Enable centering of the cover pages.
Default is `true`.

### `startPage`

Page number (>= 1) to open.
Default is `null`.

### `loadingImage`

URL of an image that is displayed while page is loading.
By default internal animated SVG is used.

### `clickToZoom`

Zoom in or out on click or tap. Default is `true`.

### `dragToFlip`

Flip page by dragging/swiping. Default is `true`.

## Events

### `flip-left-start`

Fired when flip to left animation starts. Argument is page number before flip.

### `flip-left-end`

Fired when flip to left animation ends. Argument is page number after flip.

### `flip-right-start`

Fired when flip to right animation starts. Argument is page number before flip.

### `flip-right-end`

Fired when flip to right animation ends. Argument is page number after flip.

### `zoom-start`

Fired when zoom-in/out animation starts.
Argument is magnification after zoom.

### `zoom-end`

Fired when zoom-in/out animation ends.
Argument is magnification after zoom.

## Slot props

This component exposes some properties and methods as slot properties.
Example usage:

```html
<flipbook :pages="pages" v-slot="flipbook">
  <button @click="flipbook.flipLeft">Previous Page</button>
  <button @click="flipbook.flipRight">Next Page</button>
</flipbook>
```

For more practical usage, refer to [`src/App.vue`](https://github.com/ts1/buddha-miracles-and-personal-experience/blob/master/src/App.vue) (the demo page source).

These properties and methods can also be referred through `$refs` to the `flipbook` component.

### `canFlipLeft`

True if it can flip to previous page. _NOTE_: Can return false if currently being animated.

### `canFlipRight`

True if it can flip to next page. _NOTE_: Can return false if currently being animated.

### `canZoomIn`

True if it can zoom in.

### `canZoomOut`

True if it can zoom out.

### `page`

Current page number (1 to `numPages`).

### `numPages`

Total number of pages.

### `flipLeft()`

Method to flip to previous page.

### `flipRight()`

Method to flip to next page.

### `zoomIn()`

Method to zoom in.

### `zoomOut()`

Method to zoom out.

## CSS API

You may need to specify the size of view port in your style sheet, directly to
`<flipbook>` element, or to `.viewport` sub-element of flipbook.

If the size is horizontally long and `singlePage` prop is `false` (default), it displays two pages spread, suitable for desktop browsers.
If it's vertically long, it displays single pages, suitable for smartphones.

There are some internal classes.

### `.viewport`

A `<div>` element that contains everything but `<slot>`.
`<slot>` is placed above `.viewport`.

### `.bounding-box`

Approximate bounding box of the displayed images.
Suitable to give `box-shadow`.

## Browser support

Supports modern browsers and IE 11.

## Development

To start development server with demo pages:

```
cd examples/demo
pnpm i
pnpm serve
```

To package for npm:

```
pnpm dist
```

## Credits

- vivekKodira: README correction
- siderisng: `dragToFlip`

## License

MIT

Copyright © 2019-2022 Takeshi Sone.
