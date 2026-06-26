# Free Fuel Bill Generator

A single-file, client-side web app that generates realistic Indian fuel-station
receipt mockups with a photographed / scanned thermal-paper look. Everything runs
in the browser — no backend, no build step. Open `index.html` and go.

> For design, demo and educational purposes only.

## Features

- **3 receipt templates** — IndianOil, Bharat Petroleum (BPCL), and a GST tax-invoice style.
- **Firmware-accurate layout** — fixed-width character grid (like ESC/POS), with
  right-aligned totals, fixed colon columns and word-wrapping, just like real printer firmware.
- **80 mm / 58 mm paper** — true millimeter sizing with an auto-fit font so the columns
  exactly fill the printable width.
- **Real pump logos** — IndianOil, HP and BPCL, embedded as assets.
- **6 procedural paper textures** — slight fibers, tiny wrinkles (diffuse-lighting crumple
  shading) and faded edges, generated on the fly as SVG.
- **Photographed look** — ink blends into the paper (multiply), a scan filter softens and
  warps the text, and a grain/haze pass unifies logo + text + paper into one captured image.
- **OCR auto-fill (optional)** — upload a receipt photo; text is read in-browser with
  Tesseract.js and mapped into the form. Editable text fallback for corrections.
- **Export** — download a post-processed PNG (camera/scan baked in) or print / save as PDF.

## Usage

Just open `index.html` in any modern browser (Chrome, Edge, Safari, Firefox).

To host it for free, push this repo to GitHub and enable **GitHub Pages** (Settings →
Pages → deploy from `main`, root). The app will be served at
`https://<user>.github.io/<repo>/`.

## Internet dependencies (CDN)

The app is self-contained except for three CDN resources, loaded at runtime:

- [html2canvas](https://cdnjs.com/libraries/html2canvas) — PNG export
- [Tesseract.js](https://github.com/naptha/tesseract.js) — in-browser OCR (downloads its
  engine + language data on first use, a few MB)
- Google Fonts (Share Tech Mono, Source Code Pro, VT323) — thermal fonts

An internet connection is needed for PNG export, the web fonts and OCR. The receipt
preview and printing work offline once fonts are cached.

## Project structure

```
index.html                 # the entire app (logos embedded as base64)
assets/logos/*.webp         # original logo source files
```

The logos are embedded directly in `index.html` as base64, so the app runs even without
the `assets/` folder — the files are kept here as editable source.

## Customizing the "scanned" realism

The main knobs live in `index.html`:

- `#scanInk` SVG filter — `stdDeviation` (blur) and `scale` (warp).
- `pre.r-text` and `.receipt::after` — `opacity` (ink fade and grain strength).
- `downloadPNG()` — blur / grain / vignette amounts baked into the exported PNG.

## License

MIT — see [LICENSE](LICENSE).
