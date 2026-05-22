# Design.md — Project Visual Authority


## Colors

- Dark navy base — `rgba(6, 16, 38, 0.78)`
- Cyan primary — `#7DF9FF`
- Blue secondary — `#4DA8FF`
- Blue soft (secondary labels) — `#8BC3FF`
- Text white — `#f5f9ff`
- Text off-white (sub-labels) — `#EEF8FF`
- Text ice (high-emphasis headlines) — `#DDFEFF`

Cyan-on-navy throughout. No warm hues.

---

## Typography

Font: **Inter, system-ui, sans-serif** — no other fonts.

- Display headline — 50–84 px, weight 900
- Large number — 58–84 px, weight 900
- Kicker / label — 13–19 px, weight 700–800
- Sub-label — 12–18 px, weight 600–700

Keep copy short: 1–2 words for headlines, 2–4 words for kickers. Prefer icons over sentences.

---

## Visual Aesthetic
- Liquid-glass aesthetic — every surface is a frosted glass card on a dark navy base. Cyan-on-navy palette throughout; no warm hues.
- Glass surfaces have: gradient overlay, dark navy fill, backdrop-filter blur, cyan border, inner highlight, outer glow, and a ::before shimmer layer. Each card also gets an aura bloom behind it and a light speck off one corner.
- Keep comps centrally aligned to the video canvas
- Ensure that the text is not too small or the comp is not very cramped
- Wherever icons and headlines appear together, keep them in side by side stacking (and not vertical stacking). To optimise for space and compactness.


## Icons

Lucide inline SVG, `fill="none"`, `stroke="currentColor"`. Wrap in a div with `filter: drop-shadow(0 0 16px rgba(125,249,255,0.60))`.
- Use icons effectively to communicate ideas.

---

## Motion

Timeline — 2 zones, 15 seconds total:


0 ──────────  5s   ENTRY    All animations complete here
5 ────────── 15s  AMBIENT  Compu fully visible. Aura and glass glow breathe. Nothing else.

- Trim the duration of the comps in the master index to match the context video, but set `DUR = 15` in every sub-composition — documents standalone duration, must match the timeline length.

- **Stagger all entries** — minimum 0.12 s between elements. Simultaneous multi-element entry at t = 0 is **prohibited**.
- 
- **No abrupt opacity changes** — all opacity transitions use `sine.inOut` or `power2.inOut`, minimum 0.6 s duration. Hard cuts (`duration: 0`) are **banned**.


### Sub-composition duration rules

1. Set `DUR = 15` in every sub-composition — documents standalone duration, must match the timeline length.
2. Extend breathing loops to fill the runtime: `repeat = Math.ceil((15 - startTime) / duration) - 1`. The last breathing tween anchors the timeline at ~15 s.
3. `index.html` `data-duration` values are trim points — never change them. The host element decides how much of the 15 s plays in the master; the sub-comp always runs the full 15 s.

---

## Canvas & Positioning
- Leave 20–30% clear space on all four sides so aura glow and blur dissipate without hard clipping.

---

## Project Hard Rules

- **No exit animations** — the editor cuts the clip. Nothing fades, slides, or scales out. Once on screen, everything stays.
- **Duration is always 15 s.** Never shorter than 15 s.
- **No abrupt opacity changes** — minimum 0.6 s, `sine.inOut` or `power2.inOut` only. `duration: 0` on opacity is banned.
