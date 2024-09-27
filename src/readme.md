# Modular Use

To use q5 modules, "q5.js" (the default bundle) or the "q5-core.js" module must be loaded first!

```html
<script src="https://q5js.org/src/q5-core.js"></script>
```

These modules are included in the default "q5.js" bundle:

```html
<script src="https://q5js.org/src/q5-2d-canvas.js"></script>
<script src="https://q5js.org/src/q5-2d-drawing.js"></script>
<script src="https://q5js.org/src/q5-2d-image.js"></script>
<script src="https://q5js.org/src/q5-2d-soft-filters.js"></script>
<script src="https://q5js.org/src/q5-2d-text.js"></script>
<script src="https://q5js.org/src/q5-ai.js"></script>
<script src="https://q5js.org/src/q5-color.js"></script>
<script src="https://q5js.org/src/q5-display.js"></script>
<script src="https://q5js.org/src/q5-input.js"></script>
<script src="https://q5js.org/src/q5-math.js"></script>
<script src="https://q5js.org/src/q5-sound.js"></script>
<script src="https://q5js.org/src/q5-util.js"></script>
<script src="https://q5js.org/src/q5-vector.js"></script>
```

Additional modules:

```html
<script src="https://q5js.org/src/q5-dom.js"></script>
<script src="https://q5js.org/src/q5-noisier.js"></script>
<script src="https://q5js.org/src/q5-sensors.js"></script>
```

WebGPU rendering modules are in development:

```html
<script src="https://q5js.org/src/q5-webgpu-canvas.js"></script>
<script src="https://q5js.org/src/q5-webgpu-drawing.js"></script>
```

# Module Info

- [Modular Use](#modular-use)
- [Module Info](#module-info)
  - [core](#core)
  - [canvas](#canvas)
  - [q2d-canvas](#q2d-canvas)
  - [q2d-drawing](#q2d-drawing)
  - [q2d-image](#q2d-image)
  - [q2d-soft-filters](#q2d-soft-filters)
  - [q2d-text](#q2d-text)
  - [webgpu-canvas](#webgpu-canvas)
  - [webgpu-drawing](#webgpu-drawing)
  - [webgpu-image](#webgpu-image)
  - [webgpu-text](#webgpu-text)
    - [Default Font](#default-font)
    - [Loading Custom Fonts](#loading-custom-fonts)
    - [Displaying Emojis](#displaying-emojis)
    - [Lightweight Use](#lightweight-use)
    - [Implemented functions](#implemented-functions)
  - [math](#math)
  - [noisier](#noisier)

## core

The core module provides the absolute basic functionality necessary to run q5.

It loads other modules by passing `$` (alias for `this`) and `q` (which in global mode is a proxy for `this` and `window` or `global`).

## canvas

The canvas module provides shared functionality for all canvas renderers, such as adding the canvas to the DOM, resizing the canvas, setting pixel density,

## q2d-canvas

Adds Canvas2D rendering support to q5.

All other 2D modules depend on this module.

Though loading q5-color is recommend, it's not required since `fill` and `stroke` can be set to a CSS color string.

## q2d-drawing

Adds Canvas2D drawing functions to q5.

## q2d-image

Adds Canvas2D image support to q5.

The filters in q5-image use the [CanvasRenderingContext2D.filter](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/filter) property to apply native hardware-accelerated filters to images.

## q2d-soft-filters

Software implementation of image filters.

This module includes additional filters not implemented in q5-image and legacy filter support for Safari which lacks `ctx.filter`.

These filters are slow. Real-time use of them is not recommended.

As of April 2024, Safari Technology Preview supports `ctx.filter` under a flag. Hopefully in the near future this module can be omitted from the default bundle.

## q2d-text

Adds Canvas2D text rendering support to q5.

Image based features in this module require the q5-2d-image module.

`createTextImage(str, w, h)` provides a simple way for users to create images from text.

`textImage(img, x, y)` displays text images, complying with the user's text position settings instead of their image position settings. The idea is that text will appear in the same place as it would if it were drawn with the `text` function.

`textCache(bool, maxSize)` enables or disables text caching.

## webgpu-canvas

> ⚠️ Experimental features! ⚠️

To use q5's WebGPU renderer, run `Q5.webgpu()` at the bottom of your sketch. Explicit use of `createCanvas` is required.

```js
function setup() {
	createCanvas(200, 200);
	noStroke();
}

function draw() {
	clear();
	rect(50, 50, 100, 100);
}

Q5.webgpu();
```

WebGPU has different default settings compared to q5's q2d renderer and p5's P2D and WEBGL modes.

- The default color mode is RGB in 0-1 "float" format: `colorMode(RGB, 1)`.
- The origin of the canvas (0, 0) is in the center, not the top left.
- Mouse and touch coordinates correspond to canvas pixels.
- Use `textFill` and `textStroke` to set text colors.
- For now, strokes are only implemented for the `point`, `line`, and `text` functions.

The sketches you create with the q5-webgpu renderer will still display properly if WebGPU is not supported on a viewer's browser. q5 will put a warning in the console and apply a compatibility layer to display sketches with the fallback q2d renderer.

Use of top level global mode with the WebGPU renderer requires that you make your sketch file a js module and await for `Q5.webgpu()` to return the Q5 instance (`q`), which you can then use to set q5 functions such as `draw`.

```html
<script type="module" src="sketch.js">
```

```js
let q = await Q5.webgpu();

createCanvas(200, 200);
noStroke();

q.draw = () => {
	clear();
	rect(50, 50, 100, 100);
};
```

Implemented functions:

`createCanvas`, `resizeCanvas`, `fill`, `clear`, `push`, `pop`, `resetMatrix`, `translate`, `rotate`, `scale`

## webgpu-drawing

> Uses `colorMode(RGB, 1)` by default. Changing it to 'oklch' is not supported yet for the webgpu renderer.

All basic shapes are drawn from their center. Strokes are not implemented yet.

q5's WebGPU renderer drawing functions like `rect` don't immediately draw on the canvas. Instead, they prepare vertex and color data to be sent to the GPU in bulk, which occurs after the user's `draw` function and any post-draw functions are run. This approach better utilizes the GPU, so it doesn't have to repeatedly wait for the CPU to send small chunks of data that describe each individual shape. It's the main reason why WebGPU is faster than Canvas2D.

Implemented functions:

`rect`, `circle`, `ellipse`, `triangle`, `beginShape`, `vertex`, `endShape`, `blendMode`

## webgpu-image

Implemented functions:

`loadImage`, `loadTexture`, `image`, `imageMode`

## webgpu-text

The q5 WebGPU text renderer uses the multi-channel signed distance fields (MSDF) technique for high performance and high quality real-time text rendering. Text can be rapidly recolored, rotated, and scaled without any loss in quality or performance.

MSDF, introduced by Chlumsky Viktor in his master's thesis ["Shape Decomposition for Multi-channel Distance Fields" (2015)](https://dspace.cvut.cz/bitstream/handle/10467/62770/F8-DP-2015-Chlumsky-Viktor-thesis.pdf), improves upon the signed distance field (SDF) technique, popularized by Chris Green and [Valve Software](https://www.valvesoftware.com/en/) in ["Improved Alpha-Tested Magnification for Vector Textures and Special Effects" (2007)](https://steamcdn-a.akamaihd.net/apps/valve/2007/SIGGRAPH2007_AlphaTestedMagnification.pdf).

| SDF                                                                                                                  | MSDF                                                                                                                  |
| -------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| ![demo-sdf16](https://user-images.githubusercontent.com/18639794/106391905-e679af00-63ef-11eb-96c3-993176330911.png) | ![demo-msdf16](https://user-images.githubusercontent.com/18639794/106391899-e37ebe80-63ef-11eb-988b-4764004bb196.png) |

### Default Font

For convenience, if no font is loaded before `text` is run, then q5's default MSDF font is loaded: https://q5js.org/fonts/YaHei-msdf.json

![YaHei msdf texture](https://q5js.org/fonts/YaHei.png)

This 512x512 msdf texture (207kb) was made with the [Microsoft YaHei](https://learn.microsoft.com/en-us/typography/font-list/microsoft-yahei) font and stores every character visible on a standard English keyboard, letters with diacritics (accents) used in European languages, and mathematical symbols.

```
!"#$%&'()\*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^\_`abcdefghijklmnopqrstuvwxyz{|}~¡¢£¥©®°²³´·¹º¿ÀÁÂÃÄÅÆÇÈÉÊËÌÍÎÏÐÑÒÓÔÕÖ×ØÙÚÛÜÝÞßàáâãäåæçèéêëìíîïðñòóôõö÷øùúûüýþÿ‘’“”π
```

> Do you think any other characters ought to be included in the default set? Let us know! https://github.com/q5js/q5.js/issues

### Loading Custom Fonts

You can choose a custom set of characters and convert fonts to MSDF format by using the [msdf-bmfont-xml](https://msdf-bmfont.donmccurdy.com/) website, created by Don McCurdy.

Here's how to load an MSDF font:

```js
function preload() {
	loadFont('arial-msdf.json');
}

function setup() {
	createCanvas(200, 200);
}

function draw() {
	fill(0.71, 0.92, 1);
	text('Hello, World!', mouseX, mouseY);
}

Q5.webgpu();
```

### Displaying Emojis

Full color emoji characters can't be rendered using the MSDF technique, so use `createTextImage` and display them with `textImage`:

```js
let puppy;

function setup() {
	createCanvas(200, 200);
	textSize(100);
	puppy = createTextImage('🐶');
}

function draw() {
	textAlign(CENTER, CENTER);
	textImage(puppy, 0, 0);
}

Q5.webgpu();
```

### Lightweight Use

For super lightweight use load <https://q5js.org/fonts/YaHei-256-msdf.json>, which has a limited character set of english letters and some common punctuation symbols that completely fill in a 256x256 texture (73kb).

```
!@'",-.0123456789:ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz
```

### Implemented functions

`loadFont`, `text`, `textSize`, `textAlign`, `textWidth`, `createTextImage`, `textImage`

## math

`PerlinNoise` is q5's default noise algorithm. Kevin Perlin won an Academy Award for his work on the original algorithm for the 1982 movie Tron. The JavaScript implementation of it in q5 was authored by Tezumie.

`noiseMode` enables users to switch between noise algorithms, although only "perlin" is included in q5-math.

## noisier

Adds additional noise functions to q5.

`SimplexNoise` is a simplex noise implementation in JavaScript by Tezumie. Kevin Perlin's patent on simplex noise expired in 2022. Simplex noise is slightly faster but arguably less visually appealing than perlin noise.

`BlockyNoise` is similar to p5's default `noise` function, which is a bit notorious in the gen art community for not actually being perlin noise, despite its claims to be. It looks closer to value noise but is not a standard implementation of that either. When visualized in 2d it's a bit blocky at 1 octave, hence the name. This algorithm is however, very good at outputting a variety of values from less inputs, even just a single param.
