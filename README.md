# 色重ね — IroKasane

> **Iro** (色) — color · **Kasane** (重ね) — layering, stacking

A zero-dependency, single-file color extraction and palette management app. Upload any image, extract its dominant colors via k-means clustering, organize them into primary and secondary palettes, and save them for later — all without leaving the browser.

---

## Features

**Color Extraction**
- Upload any image directly from your device 
- K-means clustering algorithm extracts up to 10 perceptually distinct colors
- Filters near-identical colors by perceptual distance to avoid duplicates
- Skips near-white and near-black pixels for more useful palette results
- Automatic color naming (Red, Orange, Cyan, Indigo, etc.)

**Palette Management**
- Palettes persist across sessions via `localStorage`
- Split view into Primary and Secondary color groups
- One-tap hex copy to clipboard
- Delete individual palettes

**About / Profile**
- Dynamic gradient banner generated from your latest saved palette's colors
- Live stats: total palettes saved and total colors across all palettes
- Links to GitHub and personal website

**UI & UX**
- Fully self-contained — one `.html` file, no build step, no server
- Mobile-first layout with `100dvh`, `max-scale=1`, and Apple PWA meta tags
- Installable as a PWA on iOS (Add to Home Screen)
- Light and dark mode with instant `0.05s` transitions, preference saved to `localStorage`
- Frosted glass nav bar and footer overlays with `backdrop-filter`
- Screen-to-screen navigation with fade + blur entrance animations
- Toast notifications for copy feedback and actions

---

## Tech

| Concern | Approach |
|---|---|
| Color extraction | Custom k-means on downsampled canvas pixel data |
| Perceptual dedup | Euclidean distance in RGB space (threshold: 50) |
| Persistence | `localStorage` (JSON serialized) |
| Fonts | Nunito via Google Fonts |
| Rendering | Vanilla HTML/CSS/JS — zero dependencies |
| PWA | Apple mobile web app meta tags |

---

## Getting Started

No install. No build. Just open the file.

```bash
# Clone
git clone https://github.com/darksudohunter/irokasane.git
cd irokasane

# Open directly in browser
open index.html
```

Or drop `index.html` on any static host (GitHub Pages, Netlify, Vercel) and it works immediately.

---

## How It Works

1. **Upload** — tap the image area to pick a file or take a photo
2. The image is drawn onto a hidden `<canvas>` at 100×100px
3. Every 8th pixel is sampled; near-white, near-black, and transparent pixels are discarded
4. K-means runs for 8 iterations with `k=24` initial centroids
5. Results are deduplicated by RGB distance, sorted by saturation, and trimmed to 10 colors
6. Colors are split at the midpoint into Primary (more saturated) and Secondary groups
7. **Save** to persist the palette, or go back and try a different image

---

## Project Structure

```
irokasane/
└── index.html   # Everything — markup, styles, and logic in one file
```

---

## License

MIT — do whatever you want with it.

---

<p align="center">Made in India with ❤️ by <a href="https://darksudohunter.dev">@Darksudohunter</a></p>
