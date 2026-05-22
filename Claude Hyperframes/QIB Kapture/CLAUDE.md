# HyperFrames Composition Project

---

## Visual Authority

**[Design.md](Design.md) is the sole authority** for canvas size, positioning, duration, motion, color, typography, and glass treatment. Read it before writing or modifying any composition.

When Design.md conflicts with the HyperFrames skill's `house-style.md`, `visual-styles.md`, layout-before-animation references, or `SECTION 2` of this file — **Design.md wins**. The other sources are advisory.

---

## SECTION 1 — HyperFrames Framework

Always invoke the relevant skill before writing or modifying compositions — skills encode framework-specific patterns that are NOT in generic web docs. Skipping them produces broken compositions.

### Skills

- **hyperframes** (`/hyperframes`) — Creating or editing HTML compositions, captions, TTS, audio-reactive animation, marker highlights
- **hyperframes-cli** (`/hyperframes-cli`) — Dev-loop CLI: init, lint, inspect, preview, render, doctor
- **hyperframes-media** (`/hyperframes-media`) — Asset preprocessing: tts (Kokoro), transcribe (Whisper), remove-background (u2net)
- **hyperframes-registry** (`/hyperframes-registry`) — Installing blocks and components via `hyperframes add`
- **website-to-hyperframes** (`/website-to-hyperframes`) — Capturing a URL and turning it into a video — full website-to-video pipeline
- **tailwind** (`/tailwind`) — Tailwind v4 browser-runtime styles for projects created with `hyperframes init --tailwind`
- **gsap** (`/gsap`) — GSAP animations for HyperFrames — tweens, timelines, easing, performance
- **animejs** (`/animejs`) — Anime.js animations registered on `window.__hfAnime`
- **css-animations** (`/css-animations`) — CSS keyframes that HyperFrames can pause and seek
- **lottie** (`/lottie`) — `lottie-web` and dotLottie players registered on `window.__hfLottie`
- **three** (`/three`) — Three.js scenes rendered from HyperFrames `hf-seek` events
- **waapi** (`/waapi`) — Web Animations API motion driven through `document.getAnimations()`

> **Skills not available?** Ask the user to run `npx hyperframes skills` and restart their session, or install manually: `npx skills add heygen-com/hyperframes`.

### Additional Skills (loaded separately — not part of the HyperFrames skill set)

These skills live in the Claude skills folder. Invoke them explicitly when the user requests the relevant output.

- **ograf-conversion** (`/ograf-conversion`) — Any time the user asks to convert, wrap, or export a composition to OGraf / DaVinci Resolve / EBU OGraf v1
- **html-to-lottie** (`/html-to-lottie`) — Any time the user wants an HTML composition translated into a Lottie JSON file

### Commands

```bash
npm run dev          # start the preview server (long-running — keep it alive in background)
npm run check        # lint + validate + inspect
npm run render       # render to MP4
npm run publish      # publish and get a shareable link
npx hyperframes lint --verbose  # include info-level findings
npx hyperframes lint --json     # machine-readable output for CI
npx hyperframes docs <topic>    # reference docs in terminal
```

> **`npm run dev` is a long-running server, not a one-shot command.** Always run it with `run_in_background: true`. Never run it as a foreground command — it will time out and kill the server.

### Documentation

```bash
npx hyperframes docs <topic>
```

Topics: `data-attributes`, `gsap`, `compositions`, `rendering`, `examples`, `troubleshooting`

Full docs index (do NOT guess URLs): `https://hyperframes.heygen.com/llms.txt`

### Project Structure

- `index.html` — main composition (root timeline)
- `compositions/` — sub-compositions referenced via `data-composition-src`
- `meta.json` — project metadata (id, name)
- `transcript.json` — whisper word-level transcript (if generated)

### Linting — ALWAYS RUN AFTER CHANGES

```bash
npm run check
```

Fix all errors before presenting the result. Inspect warnings should be reviewed before rendering.

### Framework Hard Rules

- Every timed element needs `data-start`, `data-duration`, `data-track-index`, and `class="clip"`
- Timelines must be paused and registered: `window.__timelines = window.__timelines || {}; window.__timelines['id'] = gsap.timeline({ paused: true })`
- Videos are `muted playsinline`. Audio is always a separate `<audio>` element.
- Sub-compositions are referenced via `data-composition-src="compositions/file.html"` on the host element
- `repeat: -1` is banned by the render engine — always calculate a finite repeat count
- No `Math.random()`, `Date.now()`, or any non-deterministic logic — the renderer seeks by frame
- Never build timelines inside `async`, `setTimeout`, or Promises
- `npm run check` must return 0 errors before render

---

