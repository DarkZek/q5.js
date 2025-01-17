# 1-0

## Create art with q5.js! 🎨

**q5.js** is a spiritual successor to the [p5.js](https://p5js.org) and [Processing Java](https://processing.org/) graphics libraries. ⭐️

- performance optimized for interactive art 🚀
- includes a brand new renderer powered by WebGPU 💪
- up to 32x faster than p5.js 🏎️
- HDR color support 🌈
- compatible with popular addons, including [p5.sound](https://p5js.org/reference/#/libraries/p5.sound) and [p5play](https://p5play.org) 🎮
- no dependencies, less than 100kb minified 📦
- LGPL licensed (just like p5.js) 🆓

q5.js was designed to make creative coding fun and accessible for a new generation of artists, designers, educators, and beginners. 🤝

# 1-1

If you're already familiar with p5, you'll find yourself right at home with q5. 🏡

# 2-0

## Blazing fast! 🚀

[Draw up to 32x more](https://github.com/q5js/q5.js/wiki/Developer-Log) per frame with [q5 WebGPU](https://developer.mozilla.org/docs/Web/API/WebGPU_API), compared to the limits of p5. Or save battery by getting the same results with less power consumption. 🌱

Switching from p5 to q5 is like getting a free computer upgrade. 🎉

# 3-0

## Start coding! 💻

No installation required! Use an online code editor with one of these q5.js template projects: [OpenProcessing](https://openprocessing.org/sketch/2471587), [Aijs](https://aijs.io/editor?user=quinton-ashley&project=logoSpin), or [CodePen](https://codepen.io/qashto/pen/jENEJNy). 🖌️

# 3-1

## Join our community 🤝

The future of creative coding is here! Join us on the [q5 community Discord](https://discord.gg/QuxQYwGWuB). 🙋

# 3-2

## Local development 🛠️

You can [use q5 offline](https://github.com/q5js/q5.js/wiki/Get-Started) or add this to your HTML file to always load the latest version.

```html
<script src="https://q5js.org/q5.js"></script>
```

# 3-3

## Support q5 💙

q5 is open source and anyone can use it for free under the terms of the LGPL (just like p5.js). 🎉

We need your support though! If you enjoy using q5.js, please donate via [GitHub Sponsors](https://github.com/sponsors/quinton-ashley) or [Patreon](https://www.patreon.com/q5play).

# 4-0

## More vibrant colors! 🎨

# 4-1

In p5, bright colors can look dull 😕

# 4-2

q5 empowers artists with [HDR color support](https://github.com/quinton-ashley/q5.js?tab=readme-ov-file#hdr-color-support) 🤩

# 5-0

## More help for beginners! ✨

Why doesn't this code work? `text('Hello!')` 🤔

# 5-1

p5's error messages are often too vague, leaving users searching for help. 🙋

```
🌸 p5.js says: [test.js, line 19] text() was expecting at least 3 arguments, but received only 1.
```

# 5-2

Run q5's `askAI()` before code that isn't working as expected. 🤖

```
The `text` function requires the x and y coordinates where the text should be drawn to the canvas.

text('Hello!', 50, 50);
```

# 10-0

## Dynamic 🐙

Q5 instances can be created manually, which makes the `setup` function optional. Use q5 functions anywhere with [top-level global mode](https://github.com/q5js/q5.js/wiki/Top%E2%80%90Level-Global-Mode)! 👀

```js
new Q5();

createCanvas(400, 400);
```

# 10-1

## Sound On 🔊

p5.sound is a great library, but typical use doesn't require its extensive sound generation and filtering features. 🎛️

q5.js includes sound loading, playback, and basic mixing by default. 🎚️

# 10-2

## Lightweight 🪶

p5.js and p5.sound.js have a combined size of 5.6MB! ⚠️

q5.js is only 111kb, that's 98% smaller. 🌳

For extremely lightweight use, load only the features you need from the [q5 source folder](https://github.com/q5js/q5.js/tree/main/src). 📦

# 10-3

## Frame your Art 🖼️

The `displayMode` function lets you frame your art within the browser window, no CSS skills required! 📽️

Make it "centered", "maxed", or "fullscreen" without clipping or changing the aspect ratio. Use the "pixelated" rendering preset to make pixel art. 👾

# 20-0

## Credits 🌟

This project aims to be the spiritual successor to the incredible work done by [Ben Fry](https://benfry.com) and [Casey Reas](https://x.com/REAS) on Java [Processing](https://processingfoundation.org/), [Lauren McCarthy](http://lauren-mccarthy.com)'s work on [p5.js](https://p5js.org), and all contributors to these projects.

The original [q5xjs (v0)](https://github.com/LingDong-/q5xjs) was created by [@LingDong~](https://github.com/LingDong-) and released under the public domain Unlicense license. We forked and significantly extended the unmaintained codebase.

q5.js v2 is open source under the LGPLv3, created and actively maintained by the q5 team: [@quinton-ashley](https://github.com/quinton-ashley) and [@Tezumie](https://github.com/Tezumie).

# 100

q5js.org was created by the q5 team. Copyright 2024.
