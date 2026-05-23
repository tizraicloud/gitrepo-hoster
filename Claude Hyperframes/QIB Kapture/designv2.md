# Style Reference — Liquid-Glass Infographic System

A futuristic, cyan-on-navy glassmorphism aesthetic. Every overlay is a glowing glass panel floating on a dark canvas with soft ambient halos. The look is technical but warm — heavy blur, layered transparency, and slow breathing animations give the compositions a living, holographic quality.

---

## Color Palette

### Accent Colors

| Role | Value | Usage |
|------|-------|-------|
| Cyan (primary) | `#7DF9FF` / `rgba(125,249,255,...)` | Headlines, glows, borders, icon tints, progress fills |
| Blue (secondary) | `#4DA8FF` / `rgba(77,168,255,...)` | Gradient endpoints, secondary glows, deeper accents |
| Soft Blue (tertiary) | `#8BC3FF` | Right-side / secondary panel highlights, alternate labels |

### Text Colors

| Role | Value | Usage |
|------|-------|-------|
| White | `#F5F9FF` | Primary body text |
| Off-white | `#EEF8FF` | Sub-labels, secondary copy |
| Ice | `#DDFEFF` | High-emphasis headlines |
| Pure white | `#FFFFFF` | Rare accent text |

### Background Colors

| Role | Value | Usage |
|------|-------|-------|
| Deep navy | `rgba(6, 16, 38, 0.78)` | Glass panel base fill |
| Darker navy | `rgba(4, 10, 28, 0.6–0.98)` | Kicker pill backgrounds, deeper layers |
| Black | `#000` | Video / canvas background |
| Vignette | `rgba(8, 22, 56, 0.32)` | Edge darkening on root canvas |

### Color Strategy

- **Duotone system**: Cyan + Blue, never warm hues.
- **Left/right split**: Left panels use cyan (`#7DF9FF`), right/secondary panels shift to soft blue (`#8BC3FF`).
- **Depth through transparency**: 6–8 opacity levels (0.03 to 0.78) create layered depth without additional hues.

---

## Typography

**Font**: Inter, system-ui, sans-serif — no other fonts, ever.

### Scale

| Element | Size | Weight | Letter-Spacing | Transform |
|---------|------|--------|-----------------|-----------|
| Display headline | 50–84 px | 900 | 0.01–0.04 em | UPPERCASE |
| Large number | 58–84 px | 900 | minimal | — |
| Sub-headline | 30–44 px | 900 | -0.02 em | — |
| Kicker / label | 13–19 px | 700–800 | 0.28–0.32 em | UPPERCASE |
| Sub-label | 12–18 px | 600–700 | 0.20–0.26 em | UPPERCASE |

### Text Glow (required on every text element)

```css
/* Cyan display text */    text-shadow: 0 0 22px rgba(125,249,255,0.60);
/* Headlines (large) */    text-shadow: 0 0 28px rgba(125,249,255,0.70);
/* Kicker text */          text-shadow: 0 0 10px rgba(125,249,255,0.55);
/* Off-white sub-labels */ text-shadow: 0 0 8px rgba(125,249,255,0.40);
/* Dark-backed text */     text-shadow: 0 1px 6px rgba(0,0,0,0.6), 0 0 14px rgba(125,249,255,0.5);
```

### Typographic Principles

- Keep copy extremely short: 1–2 words for headlines, 2–4 words for kickers.
- Prefer icons over sentences.
- Heavy weights only (700–900). No light or regular weights.
- Wide letter-spacing on small labels creates a tech-display feel.
- Line-height is tight on headlines: 0.96–1.04.

---

## Glass System

Every surface is built from 5 layers — never simplify or skip layers.

### Base Glass

```css
.glass {
  background:
    linear-gradient(135deg, rgba(125,249,255,0.22) 0%, rgba(77,168,255,0.10) 100%),
    rgba(6, 16, 38, 0.78);
  backdrop-filter: blur(28px) saturate(170%);
  -webkit-backdrop-filter: blur(28px) saturate(170%);
  border: 1.5px solid rgba(125,249,255,0.42);
  box-shadow:
    inset 0 1px 0 rgba(255,255,255,0.55),
    inset 0 -1px 0 rgba(77,168,255,0.14),
    0 30px 80px -20px rgba(0,0,0,0.60),
    0 0 100px rgba(125,249,255,0.32);
}
```

### Top Shine (pseudo-element)

```css
.glass::before {
  content: ''; position: absolute; inset: 0;
  background: linear-gradient(180deg, rgba(255,255,255,0.18) 0%, transparent 40%);
  border-radius: inherit; pointer-events: none;
}
```

### Border Radius by Shape

| Shape | Radius |
|-------|--------|
| Horizontal capsule | 140–170 px |
| Square / tall card | 40–44 px |
| Grid cell | 22 px |
| Pill chip / kicker | 999 px |
| Circle node | 50% |

### Border Variants

| Context | Border |
|---------|--------|
| Primary panels | `1.5px solid rgba(125,249,255,0.42–0.45)` |
| Blue-accent panels | `1.5px solid rgba(77,168,255,0.50–0.60)` |
| Pills & tags | `1px solid rgba(125,249,255,0.40)` |
| Grid cells | `1.5px solid rgba(125,249,255,0.34)` |
| Orbital rings | `1.5px dashed rgba(125,249,255,0.32)` |
| Prominent nodes | `2px solid rgba(125,249,255,0.50)` |

---

## Atmospheric Effects

### Aura (behind every glass panel)

A large blurred halo at `inset: -70px` behind the glass frame.

```css
.aura {
  position: absolute; inset: -70px;
  border-radius: 80px–200px;
  background: radial-gradient(ellipse at 50% 40%,
    rgba(125,249,255,0.30) 0%, rgba(77,168,255,0.20) 40%, transparent 72%);
  filter: blur(40px);
}
```

The ellipse center varies per composition (30% 50%, 50% 30%, 60% 40%) to break symmetry.

### Speck (one per composition)

An asymmetric light blob at a corner, partially off-frame.

```css
.speck {
  position: absolute; /* one corner, ~-50 to -80px outside the frame */
  width: 320–500px; height: 320–500px; border-radius: 50%;
  background: radial-gradient(circle, rgba(77,168,255,0.45), transparent 70%);
  filter: blur(40px);
}
```

### Vignette (root canvas)

```css
.vignette {
  position: fixed; inset: 0; z-index: 1;
  background: radial-gradient(ellipse at center, transparent 40%, rgba(8,22,56,0.32) 100%);
  pointer-events: none;
}
```

---

## Gradients Reference

### Panel & Pill Backgrounds

| Context | Gradient |
|---------|----------|
| Standard pill | `linear-gradient(135deg, rgba(125,249,255,0.22), rgba(77,168,255,0.06))` |
| Grid cell | `linear-gradient(135deg, rgba(125,249,255,0.16), rgba(77,168,255,0.03))` |
| Dark kicker pill | `linear-gradient(135deg, rgba(125,249,255,0.22), rgba(77,168,255,0.04)), rgba(4,10,28,0.6)` |
| Right-variant chip | `linear-gradient(135deg, rgba(77,168,255,0.26), rgba(43,127,255,0.05))` |

### Accent Lines & Fills

| Context | Gradient |
|---------|----------|
| Progress bar fill | `linear-gradient(90deg, #7DF9FF, #4DA8FF)` |
| Underline fade | `linear-gradient(90deg, #7DF9FF, transparent)` |

---

## Shadows Reference

### Glass Panel Shadow Stack

```
inset 0 1px 0 rgba(255,255,255,0.55)      /* top shine highlight */
inset 0 -1px 0 rgba(77,168,255,0.14)      /* bottom blue edge */
0 30px 80px -20px rgba(0,0,0,0.60)        /* deep drop shadow */
0 0 100–120px rgba(125,249,255,0.32)      /* outer cyan glow */
```

The outer glow radius increases during breathing animation (up to 180–240px).

### Icon Drop-Shadows

```css
filter: drop-shadow(0 0 16–18px rgba(125,249,255,0.60–0.65));
/* Blue variant: */
filter: drop-shadow(0 0 16px rgba(77,168,255,0.65));
```

### Special Element Shadows

| Element | Shadow |
|---------|--------|
| Node rings | `inset 0 1px 0 rgba(255,255,255,0.35), 0 0 40px rgba(125,249,255,0.4)` |
| Flow dots | `0 0 24px #7DF9FF, 0 0 44px rgba(125,249,255,0.6)` |
| Check circles | `0 0 28px rgba(125,249,255,0.35), inset 0 1px 0 rgba(255,255,255,0.3)` |
| Dot indicators | `0 0 14px #7DF9FF` |

---

## Iconography

- **Source**: Lucide icons, inline SVG.
- **Attributes**: `fill="none"`, `stroke="currentColor"`.
- **Wrapping**: Each icon sits inside a div with `filter: drop-shadow(0 0 16px rgba(125,249,255,0.60))`.
- **Node icons**: Centered in 160–180px circular containers with glass + glow treatment.

---

## Canvas & Positioning

- **Canvas**: 2560 x 1440 px (2K), always.
- **Centering**: Composition is centered both horizontally and vertically.
- **Clear space**: 20–30% on all sides so aura glow and blur dissipate without hard clipping.
- **Background**: Solid black (`#000`).

---

## Motion Language

### Timeline Structure (15 seconds)

```
0 ─────── 5s   ENTRY     All animations complete by 5s
5 ─────── 10s  HOLD      Fully visible, nothing moves
10 ────── 15s  AMBIENT   Only breathing glow, nothing else
```

### Entry Phase (0–5s)

1. **Aura** enters first — scale from 0.85, opacity fade, 0.8–0.9s.
2. **Frame / glass card** follows — y-translate + scale + opacity, 0.7s.
3. **Content elements** stagger in — minimum 0.12s between elements.
4. No simultaneous multi-element entry at t = 0.
5. No abrupt opacity changes — minimum 0.6s with `sine.inOut` or `power2.inOut`.

### Breathing Animation (starts ~1.5–3s, runs through hold + ambient)

```js
tl.to('.aura', { scale: 1.06, duration: 1.3, ease: 'sine.inOut', yoyo: true, repeat });
tl.to('.glass', {
  boxShadow: '...increased glow values...',
  duration: 1.3, ease: 'sine.inOut', yoyo: true, repeat
});
```

### Easing Guide

| Use | Easing |
|-----|--------|
| Cards & text slides | `expo.out` |
| Icon pops | `back.out(1.6–2)` |
| Breathing & ambient | `sine.inOut` |
| Secondary elements | `power2.out` |
| All opacity transitions | `sine.inOut` or `power2.inOut`, min 0.6s |

### Hard Rules

- No exit animations — the editor cuts the clip.
- Duration is always 15s (never < 10s).
- `repeat: -1` is banned — always calculate finite repeats.
- No `Math.random()`, `Date.now()`, or non-deterministic logic.

---

## Visual Identity Summary

The overall aesthetic is **holographic dark-mode glassmorphism**: panels appear to float in a void, lit from within by cyan light. The palette is intentionally narrow — only cyan and blue against deep navy — which creates visual cohesion across dozens of overlays. Every element glows. Every surface is translucent. The ambient breathing animation gives compositions a sense of life without distracting from the data. The result feels like a premium data dashboard suspended in space.
