# SCORE

SCORE is a web application that translates any uploaded image — a drawing, a photograph, a map, a doodle, a child’s painting — into a piece of music.

The core provocation is a question of notation: what is a score, and who decides what it means?

Traditional notation is a closed system: symbols with agreed meanings. SCORE inverts this. Any image becomes a valid score. The system imposes its own reading logic: position maps to time and pitch, density maps to volume, texture maps to timbre. The result is simultaneously arbitrary and structurally rigorous — which is exactly what the best graphic scores have always been.

**Format:** Web application (browser)

**Interaction:** Upload or draw → receive music

**Output:** Piano MIDI + ambient texture

**Build duration:** ~4 months

**Vibe-code difficulty:** Medium

**References:** Cardew, Cage, Fluxus

---

## Concept

Every image contains a latent piece of music. SCORE makes it audible.

Meaning in music is not inherent but constructed — and the construction can be delegated to a machine, to a stranger’s drawing, to an accident.

---

## Technical Map

The system runs in three stages: **image analysis**, **parameter mapping**, and **sound generation**. All three can run in the browser, or image analysis can optionally run on a lightweight Python server.

### Stage 1 — Image Analysis

The uploaded image is processed using:

- **Browser path:** JavaScript + Canvas API
- **Optional backend path:** Python (Pillow / OpenCV)

The image is divided into a grid. For each cell, extract:

- Average brightness
- Dominant color hue
- Edge density (how many lines/shapes)
- Vertical position

### Stage 2 — Mapping

Cell features are mapped to musical parameters.

| Visual feature | Musical parameter | Mapping |
|---|---|---|
| Horizontal position | Time | Left → right |
| Vertical position | Pitch | Top = high, bottom = low |
| Brightness | Velocity / volume | Brighter → louder |
| Edge density | Note density / rhythm | More edges → more events |
| Color hue | Timbre / effect character | Hue → instrument/effect choice |

### Stage 3 — Sound Generation

Two parallel layers are generated simultaneously.

**Layer A — Piano (MIDI sequence)**

- Built from pitch/rhythm data
- Rendered in the browser via Tone.js
- Exportable as MIDI

**Layer B — Ambient texture (generative)**

- Uses the same analyzed/mapped data
- Mapped to drone frequencies, reverb, and spectral filtering
- Rendered via Tone.js / Web Audio

---

## Core Technologies

- Tone.js
- Web Audio API
- JavaScript Canvas API
- HTML / CSS / JS frontend
- Optional backend: Python + Pillow or OpenCV
- MIDI export

---

## System Notes (Implementation Shape)

- The grid acts as the primary discretization: it turns the image into a time-ordered set of “cells” that can be interpreted as events.
- The mapping layer is the aesthetic engine: it defines the rules that make the reading feel “rigorous,” even when the input is arbitrary.
- The sound layer should preserve the distinction between:
  - a *notated* result (piano/MIDI)
  - and a *material* result (ambient texture)

---

## Scope Summary

- Browser-based experience that accepts an image upload or user drawing.
- Deterministic analysis + mapping that turns image data into:
  - Piano note events (with velocity)
  - Ambient drone/texture parameters
- Playback in-browser (Tone.js) plus MIDI export.