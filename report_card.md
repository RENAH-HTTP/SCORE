# SCORE — Project Report Card
**Theodor A. Petrea · SRH Berlin · Music Informatics 2025**
*Last updated: May 2026*

---

## What is SCORE?

SCORE is a web application that translates drawings into music. The user draws freely on a canvas (or uploads any image), and the system reads the image with computer vision — extracting visual properties like position, brightness, edge density, and colour. These properties are mapped to musical parameters (pitch, timing, velocity, timbre), and a short composition is generated and played back in the browser. The result can be exported as a MIDI file or varied with a single button.

The project draws on the tradition of graphic scores (Cardew, Cage, Fluxus) — the idea that any mark on paper can be a musical instruction — and delegates the interpretation to a machine.

---

## Project Status

| Area | Status | Notes |
|------|--------|-------|
| Concept & documentation | ✅ Done | Fully defined |
| Canvas drawing interface | 🔄 Not started | Frontend — HTML/CSS/JS |
| Image analysis function | 🔄 Not started | Grid → brightness, hue, edges |
| Parameter mapping rules | 🔄 Not started | Artistic core decision |
| Tone.js audio output | 🔄 Not started | Piano layer + drone layer |
| MIDI export | 🔄 Not started | midi-writer-js |
| Variation button | 🔄 Not started | Randomise parameters |
| Deployment | 🔄 Not started | GitHub Pages |

---

## Learning Log

### Week –2 to –1 (approx. last 2 weeks)

**Processing / p5.js**
- Started studying with The Coding Train (Daniel Shiffman, YouTube)
- Covered: setup/draw loop, shapes, variables, mouse interaction
- Key insight: the canvas coordinate system and how to read pixel data — directly relevant to SCORE's image analysis stage
- Status: ~35% comfortable. Need more practice with image pixel manipulation (`pixels[]` array, `get()` function)

**JavaScript**
- Working through basics in parallel: variables, functions, DOM manipulation, event listeners
- Learned how the Canvas API works (`getContext('2d')`, `getImageData()`)
- Status: ~25%. Enough to read and modify examples; not yet fluent writing from scratch

**Python**
- Started learning Python as an optional backend option
- Covered: syntax basics, functions, working with libraries (pip)
- Looked at Pillow for image processing — opened an image, read pixel values
- Status: ~20%. Will use for image analysis prototyping before porting to JS

**Resources in use**
- The Coding Train — Processing / p5.js playlist (Daniel Shiffman)
- MDN Web Docs — JavaScript Canvas API reference
- Python.org official tutorial
- Pillow (PIL) documentation

---

## Technical Architecture (planned)

```
[ Canvas / Image Upload ]
         ↓
[ Image Grid Analysis ]
  - Divide into 16×8 cells
  - Per cell: avg brightness, dominant hue, edge density, Y position
         ↓
[ Parameter Mapping ]
  - X position  → note onset time (0 to 8 bars)
  - Y position  → MIDI pitch (C2–C6)
  - Brightness  → velocity (ppp–fff)
  - Edge density → note density / rhythm
  - Hue          → timbre / instrument voice
         ↓
[ Sound Generation — Tone.js ]
  - Layer A: piano MIDI sequence
  - Layer B: ambient drone / texture
         ↓
[ Output ]
  - Browser playback
  - MIDI export (.mid)
  - Variation button
```

---

## Mapping Rules (draft — to be refined)

These are the core artistic decisions for the project. They will be documented properly once tested.

| Visual | Musical | Scale |
|--------|---------|-------|
| Horizontal X | Time | Column 1–16 = beats 1–16 |
| Vertical Y | Pitch | Top = C6, Bottom = C2 |
| Pixel brightness | Velocity | 0–255 → 10–127 |
| Edge density | Note duration | Low = whole notes, High = 16th notes |
| Dominant hue | Instrument | Blues = piano, Reds = strings, Greens = drone |
| Texture complexity | Reverb mix | 0–1 mapped to texture score |

---

## References

- Cornelius Cardew — *Treatise* (1963–67): graphic score as open notation
- John Cage — *Music of Changes*: chance operations in composition
- Fluxus event scores: language and image as musical instruction
- Tone.js documentation — https://tonejs.github.io
- midi-writer-js — https://github.com/grimmdude/MidiWriterJS
- The Coding Train — https://thecodingtrain.com

---

## Next Actions (prioritised)

1. Build basic canvas drawing page (HTML/CSS/JS) — just the interface, no audio yet
2. Write `analyseGrid(imageData)` function — returns array of per-cell data
3. Write out mapping rules explicitly before coding them
4. Get Tone.js playing a single note, then a sequence
5. Wire analysis → mapping → playback end-to-end with a test image
6. Add MIDI export once playback works
7. Deploy to GitHub Pages and record demo

---

*This file is a living document. Update after each work session.*
