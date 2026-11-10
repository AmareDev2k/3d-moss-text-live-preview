<div align="center">

# 3D Moss Text

**Type a phrase. Watch it grow into living moss and flowers. Brush it aside with your cursor.**

A real-time WebGL text effect built with Three.js, opentype.js and custom GLSL shaders, with a one-click export to a ready-to-use Next.js component.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Open%20Preview-7a9a12?style=for-the-badge&logo=githubpages&logoColor=white)](https://amaredev2k.github.io/3d-moss-text-live-preview/)

![Three.js](https://img.shields.io/badge/Three.js-r128-000000?style=flat-square&logo=threedotjs&logoColor=white)
![WebGL](https://img.shields.io/badge/WebGL-GLSL%20Shaders-990000?style=flat-square&logo=webgl&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-CDN-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![Next.js](https://img.shields.io/badge/Export-Next.js%20Component-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![GitHub Pages](https://img.shields.io/badge/Hosted%20on-GitHub%20Pages-222222?style=flat-square&logo=github&logoColor=white)
[![Stars](https://img.shields.io/github/stars/AmareDev2k/3d-moss-text-live-preview?style=flat-square&color=c9e04a)](https://github.com/AmareDev2k/3d-moss-text-live-preview/stargazers)

</div>



https://github.com/user-attachments/assets/303f3e42-dadf-4e7c-8a0e-2b4714fc1bb7



---

## Overview

3D Moss Text turns any phrase into a three-dimensional block of lettering that is covered in thousands of instanced moss blades and flowers. The default phrase is "Crafted for the roads of Sri Lanka", and the colour palettes are inspired by Sri Lankan landscapes.

Everything runs in the browser. There is no build step and no backend. The page is a single self-contained HTML file.

**Live preview:** https://amaredev2k.github.io/3d-moss-text-live-preview/

## Features

- **Vector text to 3D geometry.** Glyph outlines are parsed with opentype.js, converted to Three.js shapes, and extruded into a soil base.
- **Thousands of moss blades and flowers.** Surface points are sampled across the letterforms and rendered with GPU instancing, so the density stays smooth in real time.
- **Custom GLSL shaders.** Grow-in animation with easing, wind sway, and colour gradients are all computed in the vertex and fragment shaders.
- **Interactive cursor brush.** Move the pointer over the letters and the moss and flowers part around it. Cursor velocity affects how strongly they are pushed.
- **Floating petals.** Loose petals drift across the scene, react to the wind, and are pushed away by the cursor.
- **Live statistics.** The header shows the current number of moss blades, flowers and floating petals.
- **Next.js export.** One click generates the full `MossText.jsx` component with your current settings and copies it to the clipboard.

## Controls

| Control | Description | Range |
| --- | --- | --- |
| Custom Text Phrase | Any text to render | free text |
| Line Wrapping | 2-line stacked or 1-line wide layout | 2 modes |
| Font Face | Instrument Serif (luxury) or Plus Jakarta Bold (thick moss) | 2 fonts |
| Flora Palette | Ella Lush, Golden Tea, Mist Bloom | 3 presets |
| Animation Speed | Speed of the grow-in and motion | 0.2x to 2.5x |
| Cursor Brush | How strongly the cursor bends the moss | 0x to 2.5x |
| Wind Sway | Intensity of the wind movement | 0x to 2.5x |
| Floating Petals | Number of drifting petals | 0 to 10 |

Use **Replay Grow Animation** to watch the moss grow in again from the beginning.

## Palettes

| Preset | Mood |
| --- | --- |
| Ella Lush | Fresh green moss with pink blossoms |
| Golden Tea | Warm olive and gold, inspired by Ceylon tea country |
| Mist Bloom | Cool emerald with violet flowers, inspired by Horton Plains |

## How It Works

1. **Font loading.** The selected font is fetched and parsed with opentype.js, with fallback URLs if the first source fails.
2. **Outline to shape.** Each glyph path is converted into `THREE.Shape` objects, and counters such as the inside of an "o" are handled as holes.
3. **Surface sampling.** The filled shapes are triangulated, and random points are sampled across the faces and along the rim to place moss and flowers.
4. **Instancing.** Each blade and flower is one instance with per-instance position, direction and data (scale, rotation, delay, seed), drawn through `InstancedBufferGeometry`.
5. **Shaders.** The vertex shaders handle growth, wind sway and cursor displacement. The fragment shaders blend base, mid and tip colours along each blade.
6. **Pointer interaction.** The pointer is raycast onto the text plane, and its position and velocity are sent to the shaders as uniforms.

## Run Locally

The project is a single HTML file, so there is nothing to install.

```bash
git clone https://github.com/AmareDev2k/3d-moss-text-live-preview.git
cd 3d-moss-text-live-preview
```

Open the HTML file in a modern browser with WebGL support. If your browser blocks font loading from `file://`, serve the folder with any static server:

```bash
npx serve .
```

An internet connection is needed on first load because Three.js, opentype.js, Tailwind and the fonts are loaded from CDNs.

## Use It in Your Next.js Project

1. Open the live preview and adjust the settings until it looks right.
2. Click **Copy Next.js Code**. The full component is copied to your clipboard.
3. Save it as `components/MossText.jsx` and install the dependencies:

```bash
npm install three opentype.js
```

4. Use it in any client page:

```jsx
import MossText from "@/components/MossText";

export default function Hero() {
  return (
    <MossText
      text="Crafted for the roads of Sri Lanka"
      multiLine
      height={420}
    />
  );
}
```

### Component Props

| Prop | Type | Default | Description |
| --- | --- | --- | --- |
| `text` | `string` | current phrase | Text to render |
| `fontUrl` | `string` | selected font | URL of a `.ttf` or `.woff` font file |
| `height` | `number` | `420` | Canvas height in pixels |
| `multiLine` | `boolean` | from preview | Stack the text over two lines |
| `animSpeed` | `number` | from preview | Animation speed multiplier |
| `brushStrength` | `number` | from preview | Cursor brush strength |
| `windStrength` | `number` | from preview | Wind sway intensity |
| `petalCount` | `number` | from preview | Number of floating petals |
| `colors` | `object` | selected palette | Moss, flower, petal and soil colours |
| `className` | `string` | `""` | Extra class names for the canvas |

The exported component starts with `"use client"` because it uses browser-only WebGL APIs.

## Tech Stack

- [Three.js](https://threejs.org/) r128 for rendering
- [opentype.js](https://opentype.js.org/) 1.3.4 for font outline parsing
- GLSL vertex and fragment shaders
- [Tailwind CSS](https://tailwindcss.com/) (CDN) for the interface
- Fonts: Instrument Serif, Plus Jakarta Sans, Inter

## Browser Support

Any modern browser with WebGL support (Chrome, Edge, Firefox, Safari). Performance depends on the GPU, and very long phrases create more geometry, so the 2-line layout is recommended for them.

## Author

**Aravinda Amarasingha**
GitHub: [@AmareDev2k](https://github.com/AmareDev2k)

If you like this project, consider giving it a star.
