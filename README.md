# Design Me

**See it. Select it. Design Me.**

An AI design remixing platform: find an image you like, select the parts of it you want, and apply that style to your own image. Instead of asking you to know what font, palette, texture or effect was used, Design Me lets you click what you like.

The interaction model is **Find → Select → Copy → Apply → Edit**.

Traditional design tools ask *"what do you want to create?"*. Design Me asks *"what do you like?"*

---

## Running it

There is no build step and no dependencies. Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

Everything ships in that one file — CSS, JS, the mascot, the poster artwork, and the reference photographs as `data:` URIs. Fonts are the only external request (Google Fonts).

---

## What's in the repo

```
index.html                          the whole app, standalone
assets/                             the three reference photographs, originals
docs/image-transformation-rules.md  face and identity preservation policy
```

`assets/` holds the source files for the photographs that are inlined in `index.html`. They are kept separately so they can be re-encoded or swapped without digging through base64.

---

## The pages

| Route | What it is |
|---|---|
| `#home` | Hero, feature cards, *More Than Just Edits*, Explore preview, pricing, community |
| `#explore` | Masonry discovery gallery, 20 categories, live search, upload |
| `#workspace` | The core product screen — Reference / Your image / Result |
| `#library` | My Designs, My References, Saved Inspiration, My Styles |
| `#profile` | Creator profile and grids |

### The workspace

Three panels on one line:

**1 · Reference** → **2 · Your image** → **3 · Result**

- The reference is interactive. Hover to detect regions, click to select. Each reference carries a hotspot map naming its own parts — the Bloom cover knows about its glasses, masthead and issue number.
- **Copy All** transfers the reference's whole treatment. It does *not* recreate the reference image.
- Selective copying: click any region for a contextual menu — Copy Style, Copy Texture, Copy Text Style, Change Colour, Replace, Remove, Apply to My Image.
- **Design** runs the reference's recipe against your uploaded photo and builds the result beside it. Your original is never written to.
- The inspector switches by selection: a full typography panel (8 families, weight, size, spacing, line height, alignment, transform, effects, layered colour) or object editing (colour, material, shape).
- The assistant parses plain instructions — *"make the cap black"*, *"change the text to LAGOS"*, *"add grain"* — scoped to Selected / Section / Entire Design.

### Style recipes

Every reference declares what it does to an image: finish, type treatment, palette, effects, motion, and an `apply` block of concrete parameters. This drives the *What this reference does* panel and is the right shape to hand to an image model later as a prompt payload.

---

## Face and identity preservation

**Design Me changes the design around the user, not who the user is.**

An uploaded photo is the primary subject and its facial identity outranks every other constraint. The reference person's face is never transferred. Selecting a person opens a chooser — their hat, their clothing, their colour treatment, their composition — with face and identity locked behind an explicit opt-in.

In this build the guarantee is implemented by compositing the untouched original face pixels back over the styled result through a soft elliptical mask, controlled by the **Keep my face** lock. Full policy in [`docs/image-transformation-rules.md`](docs/image-transformation-rules.md).

> When a real image model is wired in, the face mask must become a hard server-side constraint on generation. A client-side composite is a prototype of the guarantee, not enforcement of it.

---

## Status

This is a working front-end prototype of the full interaction model. The transformations are real and visible, but they are **CSS filters, masks and composites — not a generative model**. Saturation, contrast, grain, halftone, dither, scanlines, gloss, colour and typography all genuinely apply to your uploaded photo. Turning a photo into, say, a glossy 3D render needs an image model behind the recipe.

Built against the MVP scope:

- [x] Inspiration gallery with categories
- [x] Upload your own reference
- [x] Upload your own image
- [x] Side-by-side workspace
- [x] Copy All
- [x] Visual click-to-select on the reference
- [x] Copy selected style
- [x] Text style extraction and editable text
- [x] Object and colour editing
- [x] AI instruction bar with scope
- [ ] Export (button is present; wiring is stubbed)
- [ ] Real segmentation, OCR, font recognition, generative editing

---

## Brand

Forest `#064B24` · hero panel `#1A5730` · ink `#0B2F1B` · cream `#FAF8ED` · pastel `#E8F1D8` · sage `#EEF4E5` · mascot green `#62C82B` · lime `#9BE86A`

Type: **Caveat Brush** for the wordmark, Caveat for headings and annotations, Patrick Hand for doodles, DM Sans for UI, Anton / Archivo Black / Bebas Neue / Playfair Display / Space Mono for poster artwork.

**Demi**, the mascot, is a fixed brand asset — hand-authored inline SVG with three props (`pencil`, `magnifier`, `none`). Same character everywhere; do not redesign him.

---

## Note on the reference images

The photographs in `assets/` are design work by other people, kept here as references. This repository is private for that reason. Clear the licensing before making it public or shipping these images in anything user-facing.
