# Motion Synthesizer

A browser-based motion design tool for creating animated particle systems, 3D mesh visuals, and typographic motion — built for experienced designers who want direct control and fast iteration.

Runs entirely in a single HTML file. No install, no server, no dependencies to manage.

![Motion Synthesizer](https://img.shields.io/badge/WebGL-PixiJS_v7-blue) ![Export](https://img.shields.io/badge/Export-MP4_%2F_WebM-green) ![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## Overview

Motion Synthesizer generates grid-based oscillating systems — wave-propagated shapes, 3D particle meshes, typographic layouts — in a style influenced by motion designers like Mario de Meyer, dvdp, and play_sf. Every parameter is animatable, every animation is phaseable, and the whole thing exports frame-accurate MP4.

---

## Features

### Shapes
15 shape types: `circle` `ellipse` `square` `rect-w` `rect-t` `roundrect` `triangle` `hexagon` `diamond` `star` `ring` `cross` `dot` `text` `marker`

### Layouts
10 layout modes that define how shapes are distributed across the canvas:

| Layout | Description |
|---|---|
| `grid` | Rows × columns with spacing control |
| `honeycomb` | Offset grid with staggered rows |
| `radial` | Evenly spaced around a circle |
| `circle-pack` | Packed circular fill |
| `text-pack` | Shapes masked to a text outline |
| `scatter` | Random distribution with seed control |
| `row / column` | Single-axis linear layouts |
| `diagonal` | Angled linear arrangement |
| `obj-mesh` | Shapes projected onto a 3D point cloud |

### Animation System
Two animation modes per track:

- **Oscillate** — continuous sine-wave motion driven by frequency. Set min/max values, frequency (Hz), and phase spread
- **Keyframe** — eased from/to with duration, delay, and loop modes (`loop`, `pingpong`, `none`)

**Animatable properties:**
`scale` `scaleX` `scaleY` `rotate` `rotDeg` `moveX` `moveY` `opacity` `skewX` `skewY` `spread` `spreadX` `spreadY` `orbitAngle` `orbitRadius` `colorCycle` `colorHue` `colorGrad` `colorRandom` `textSpacing` `mesh3dRotX` `mesh3dRotY` `mesh3dRotZ` `mesh3dScale` + all FX parameters

**Group-level:** `gMoveX` `gMoveY` `gScale` `gScaleX` `gScaleY` `gRotate`

### Phase Propagation
Each animation track has independent phase control that determines how the motion spreads across shapes:

`wave` `wave-x` `wave-y` `diagonal` `center-out` `inside-out` `sequential` `radial` `random`

### Easing
`linear` `easeInOut` `easeIn` `easeOut` `sine` `circ` `elastic` `bounce` `back`

### 3D Mesh System
Shapes can be distributed across a 3D point cloud and live-reprojected every frame:

**9 primitives:** Sphere · Icosphere · Box · Tube · Torus · Cone · Plane · Helix · Möbius

**3D deformers** (stackable): Twist · Bend · Noise · Wave · Taper · Inflate

**3D text mesh:** Rasterizes any loaded font to a pixel point cloud and extrudes it in 3D with uniform density. No external font fetching — uses fonts already loaded in the page.

**OBJ import:** Load any `.obj` file as a custom mesh source.

### Post-Processing FX
10 per-group filters with fully animatable parameters:

| Effect | Filter |
|---|---|
| Glow | Outer/inner glow with quality control |
| Bloom | Advanced bloom with threshold and scale |
| RGB Split | Chromatic aberration (X/Y offset per channel) |
| Blur | Kawase blur |
| CRT | Scanlines, curvature, noise, vignette |
| Glitch | Slice-based digital glitch |
| Radial Blur | Zoom blur from a center point |
| Tilt Shift | Gradient focus blur |
| Bulge / Pinch | Lens distortion |
| Old Film | Sepia, noise, scratch, vignette |

### Color System
- **Palette mode** — cycle through a list of colors per shape
- **Gradient mode** — multi-stop gradient mapped across the group with phase-driven distribution
- Per-shape color animation: `colorCycle` `colorHue` `colorGrad` `colorRandom`

### Motion Trails
Each group can have a motion trail with: segment count, time step, thickness, taper, smooth interpolation, color, opacity, and dash/gap pattern.

### Background
Solid color or animated multi-stop gradient with rotate or hue-cycle animation modes.

### Export
| Format | Method | Notes |
|---|---|---|
| MP4 | WebCodecs API + mp4-muxer | Frame-accurate, high bitrate. Requires Chrome 94+ |
| WebM | MediaRecorder + captureStream | Broad browser support |

Export at any canvas size and frame rate. Timeline duration is configurable.

### Canvas Sizes
Presets for 16:9 · 1:1 · 9:16 · 3:4 · 2:3 at common resolutions up to 2560×1440. Custom sizes supported.

### Frame Rates
24 / 30 / 60 fps

---

## Getting Started

1. Download `index-v7.html`
2. Open it in Chrome (Chrome recommended for MP4 export)
3. Click any preset in the left panel to start
4. Select a group → use the right panel tabs (Shape / Layout / Color / Motion) to adjust
5. Hit **▶ WebM** or **▼ MP4** to export

No build step. No internet connection required after initial load (fonts are loaded from Google Fonts on first open).

---

## Architecture

Built on:
- **PixiJS v7** — WebGL 2D rendering via manual ticker
- **WebCodecs API** — frame-accurate MP4 encoding via `VideoEncoder` + `mp4-muxer`
- **PIXI.RenderTexture** — offscreen GL framebuffer for export (avoids WebGL buffer swap read-back issues)
- **Canvas 2D** — text-to-mesh rasterization for 3D text
- Vanilla JS, no framework

All state is a single `S` object. Groups serialize to JSON and save to `localStorage` as user presets.

---

## Presets

Comes with 50+ built-in presets demonstrating the range of the system — from simple 2D grids to 3D mesh objects, text layouts, and procedural motion systems. Your own presets can be saved from the **+ Save** button in the groups panel.

---

## Browser Support

| Browser | Live Preview | MP4 Export | WebM Export |
|---|---|---|---|
| Chrome 94+ | ✅ | ✅ | ✅ |
| Firefox | ✅ | ❌ | ✅ |
| Safari | ✅ | ❌ | ⚠️ |

MP4 export requires the WebCodecs API. Use Chrome for full functionality.

---

## License

MIT
