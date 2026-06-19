# Surf Coach — Design System
# Version 1.0 — June 2026
# Source of truth for all HTML pages in the system

---

## Design intent

All HTML pages in this system share a single visual language. The mood is **calm, clear, present** — like morning light through a linen curtain. Open, unhurried, everything in its place. Opening any page should feel like a relief, not a task.

The athlete is 35 years old, living in Lisboa, training with specific goals and a specific calendar. He consults these pages on his phone before surf sessions, at the gym, at the supermarket, and at his desk on Sunday evenings. Every design decision must serve one of these four contexts.

**This file is the single source of truth.** Both `private/data/plans/template-spec.md` and `private/data/sessions/session-report-spec.md` inherit from here. When this file changes, all page specs are affected on the next generation cycle.

---

## 1. Colour Palette

All colours are defined as CSS custom properties in `:root`.

### Light mode (default)

```css
:root {
  /* Backgrounds */
  --bg:             #F7F5F2;  /* Page background — warm off-white, not pure white */
  --surface:        #FFFFFF;  /* Card / section background */
  --surface-raised: #F4F2EF;  /* Elevated state, today highlight, hover */
  --border:         #E8E4DF;  /* Dividers, card borders — barely visible */
  --bg-band:        #F2F0EC;  /* Cluster/section background variation — ~3% darker than bg */

  /* Text */
  --text-primary:   #2C2A27;  /* Main readable text — dark warm charcoal, not pure black */
  --text-secondary: #8A8480;  /* Labels, metadata, secondary info */
  --text-muted:     #B8B4AF;  /* De-emphasised: completed items, footnotes */

  /* Accent colours — three functional accents only, all desaturated */
  --accent-surf:      #4A90A4;  /* Surf sessions — calm desaturated ocean */
  --accent-gym:       #C17B5C;  /* Gym sessions — muted warm terracotta */
  --accent-recovery:  #6B9E7A;  /* Recovery, mobility, rest — soft sage green */
  --accent-alert:     #C4856A;  /* Coach/psychology notes — muted dusty sienna */

  /* Tag backgrounds — very light tints of accent colours */
  --tag-surf-bg:      #EBF4F7;
  --tag-gym-bg:       #F9F0EB;
  --tag-recovery-bg:  #EEF5F0;

  /* Domain tag colours (advice cards, specialist domains) */
  --tag-mental-color:   #9B8FC4;  /* Soft lavender */
  --tag-sleep-color:    #7B8FC4;  /* Muted indigo */
  --tag-habit-color:    #C4A46A;  /* Warm amber */
  --tag-clinical-color: #C4856A;  /* Matches --accent-alert */

  /* Shadows */
  --shadow-card:  0 1px 3px rgba(0,0,0,0.06), 0 1px 2px rgba(0,0,0,0.04);
  --shadow-today: 0 2px 8px rgba(0,0,0,0.09);
}
```

### Dark mode

Activated via `@media (prefers-color-scheme: dark)` only — no manual toggle, no class switching. The palette is **dusk at the beach**: warm-dark, not cold-dark. Elevation is expressed through surface lightness (lighter = higher), not shadows.

```css
@media (prefers-color-scheme: dark) {
  :root {
    --bg:             #1A1816;  /* Deep warm almost-black — dusk sand */
    --surface:        #242220;  /* Cards — warm dark */
    --surface-raised: #2C2A27;  /* Elevated state */
    --border:         #3A3733;
    --bg-band:        #1E1C1A;

    --text-primary:   #EAE6E1;  /* Warm off-white */
    --text-secondary: #C0BBB5;
    --text-muted:     #A8A49E;

    /* Accents brightened 15-20% for dark bg legibility */
    --accent-surf:      #6AAFC4;
    --accent-gym:       #D4956E;
    --accent-recovery:  #82B890;
    --accent-alert:     #D49880;

    --tag-surf-bg:      #1C3040;
    --tag-gym-bg:       #3A2318;
    --tag-recovery-bg:  #1A2E20;

    --tag-mental-color:   #B0A4D8;
    --tag-sleep-color:    #9AA4D8;
    --tag-habit-color:    #D8B87A;
    --tag-clinical-color: #D49880;

    --shadow-card:  0 1px 3px rgba(0,0,0,0.40), 0 1px 2px rgba(0,0,0,0.30);
    --shadow-today: 0 2px 8px rgba(0,0,0,0.60);
  }

  /* Sticky nav background */
  .sticky-nav {
    background: rgba(26, 24, 22, 0.92);
  }

  /* Habit reminder block */
  .habit-reminder {
    background: #2A2010;
    border-color: #4A3820;
  }
}
```

### Colour rules

- **Three functional accents only.** Surf = blue, gym = terracotta, recovery/rest = sage. Colour encodes activity type — it is never decorative.
- **No gradients. No wave imagery.**
- **No additional colours** without updating this file first.

---

## 2. Typography

### Font stack

**Primary (all UI):** `Inter` — loaded from Google Fonts, weights 400/500/600 only. Weight 700 is not used.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
```

**Exception — Coach/Psychology text:** `Georgia, 'Times New Roman', serif` — system font, no external load. Used for the coach's note and psychology/mindset sections. Signals "read slowly" without extra styling. Section headers within these cards remain Inter.

### Type scale

| Role | Size | Weight | Transform | Notes |
|------|------|--------|-----------|-------|
| Page title | 22px | 600 | — | Athlete name, page heading |
| Section header | 12px | 500 | uppercase | letter-spacing: 0.12em — quiet stamp |
| Card title / day label | 16px | 600 | — | — |
| Body text | 14px desktop / 15px mobile | 400 | — | — |
| Coach/psychology body | 15px | 400 | — | Georgia serif, line-height 1.75 |
| Label / tag | 11px | 500 | uppercase | letter-spacing: 0.06em |
| Metadata | 12px | 400 | — | `--text-secondary` |

**Mobile breakpoint for body text:** `@media (max-width: 640px) { body { font-size: 15px; } }`

### Line heights

- Body text: **1.7** (generous — readability on mobile)
- Coach/psychology body: **1.75** (most generous — slowest read)
- Compact metadata: **1.4**

---

## 3. Borders, Elevation & Spacing

### Border radius

- **Cards:** 12px
- **Tags, inline badges:** 6px
- **Images in grids:** 8px

### Elevation

Cards use `box-shadow` for elevation, not hard borders. Hard border retained as fallback for print/accessibility.

```css
.card {
  background: var(--surface);
  border-radius: 12px;
  border: 1px solid var(--border);
  box-shadow: var(--shadow-card);
  padding: 20px;
}
```

Today/active state uses `--shadow-today` and `--surface-raised` background.

### Left border accent

Used on cards that encode an activity type (surf, gym, recovery) or a register shift (coach note, psychology).

```css
border-left: 3px solid rgba(74, 144, 164, 0.70); /* --accent-surf at 70% */
```

Priority/emphasis variant: `4px` border.

Dark mode overrides (hardcoded rgba must be replaced):
```css
@media (prefers-color-scheme: dark) {
  .card--surf     { border-left-color: rgba(106, 175, 196, 0.70); }
  .card--gym      { border-left-color: rgba(212, 149, 110, 0.70); }
  .card--recovery { border-left-color: rgba(130, 184, 144, 0.70); }
  .card--alert    { border-left-color: var(--accent-alert); }
}
```

### Spacing

| Element | Value |
|---------|-------|
| Card padding | 20px |
| Card gap in grids | 12px |
| Section margin-top | 48px |
| Section margin-bottom (header) | 20px |
| Page horizontal padding | 16px mobile / 32px desktop |

---

## 4. Shared Components

These components appear across multiple page types and must be implemented identically.

### SectionHeader

Used to open every major section.

```css
.section-header {
  font-size: 12px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--text-secondary);
  margin-top: 48px;
  margin-bottom: 20px;
}
```

### Tag / Pill

Small inline label for activity type, domain, or status.

```css
.tag {
  display: inline-flex;
  align-items: center;
  padding: 3px 8px;
  border-radius: 6px;
  font-size: 11px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.06em;
}
.tag--surf     { background: var(--tag-surf-bg);     color: var(--accent-surf); }
.tag--gym      { background: var(--tag-gym-bg);      color: var(--accent-gym); }
.tag--recovery { background: var(--tag-recovery-bg); color: var(--accent-recovery); }
.tag--mental   { background: #EEE9F5; color: var(--tag-mental-color); }
.tag--sono     { background: #E9ECF5; color: var(--tag-sleep-color); }
.tag--habito   { background: #F5EFE0; color: var(--tag-habit-color); }
.tag--clinico  { background: #F5EBE6; color: var(--tag-clinical-color); }
```

Dark mode tag overrides:
```css
@media (prefers-color-scheme: dark) {
  .tag--mental  { background: #252038; }
  .tag--sono    { background: #1C2038; }
  .tag--habito  { background: #2E2410; }
  .tag--clinico { background: #2E1A10; }
}
```

### CoachNoteCard

The most important element on any page where the coach speaks directly. Uses Georgia serif and `--accent-alert` left border to signal "read this slowly."

```css
.coach-note-card {
  background: var(--surface);
  border-radius: 12px;
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent-alert);
  box-shadow: var(--shadow-card);
  padding: 20px;
}
.coach-note-card p {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 15px;
  font-weight: 400;
  line-height: 1.75;
  color: var(--text-secondary);
}
```

### RatingDisplay

Three large numbers side by side, used for overall / conditions / surfing ratings.

```css
.ratings-row {
  display: flex;
  gap: 0;
  border: 1px solid var(--border);
  border-radius: 12px;
  overflow: hidden;
}
.rating-item {
  flex: 1;
  text-align: center;
  padding: 16px 12px;
  border-right: 1px solid var(--border);
}
.rating-item:last-child { border-right: none; }
.rating-value {
  font-size: 28px;
  font-weight: 600;
  color: var(--text-primary);
}
.rating-label {
  font-size: 11px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  color: var(--text-muted);
  margin-top: 4px;
}
```

### StatusPill

Colour-coded status indicator. Used in goal checks and recovery state.

| Status | Background | Text |
|--------|-----------|------|
| ATINGIDO / READY | `--tag-recovery-bg` | `--accent-recovery` |
| PARCIAL / BUILD | `--tag-surf-bg` | `--accent-surf` |
| SEM TRABALHO / REST | `--surface-raised` | `--text-muted` |
| RECOVERING | amber `#F5EDD0` | `#C4A030` |

---

## 5. Page Layout Rules

### Max width & centering

```css
.page-wrapper {
  max-width: 720px;
  margin: 0 auto;
  padding: 0 16px;
}
```

Large screen (≥1280px) expands to `max-width: 1800px` — see the weekly plan spec for the full two-column grid definition. Session reports do not use the large-screen grid.

### Mobile-first

Base styles target mobile. Desktop enhancements via `@media (min-width: 640px)` and `@media (min-width: 900px)`.

Minimum touch target: **44×44px** for all interactive elements (nav links, checkboxes, accordion toggles).

### Scroll margin

All anchor targets: `scroll-margin-top: 64px` to account for sticky nav height.

---

## 6. Interaction Patterns

### Accordion (no JavaScript)

Use native `<details>/<summary>` for all collapsible content. No JavaScript required.

```html
<details class="accordion">
  <summary class="accordion__trigger">Session details</summary>
  <div class="accordion__content">...</div>
</details>
```

```css
.accordion__trigger { min-height: 44px; padding: 16px 20px; cursor: pointer; }
.accordion__trigger::-webkit-details-marker { display: none; }
```

### Checkboxes (shopping lists, recovery tracking)

Native `<input type="checkbox">` wrapped in `<label>` to expand tap area. State persisted via `localStorage` keyed by page (`STORAGE_KEY = 'surf-coach-YYYY-WNN-shopping'`).

```css
@media (prefers-color-scheme: dark) {
  input[type="checkbox"] { background: var(--surface); border-color: var(--border); }
  input[type="checkbox"]:checked { background: var(--accent-recovery); border-color: var(--accent-recovery); }
}
```

---

## 7. Print Styles

Only the shopping list section prints. All other sections: `display: none`.

```css
@media print {
  body * { visibility: hidden; }
  #section-compras, #section-compras * { visibility: visible; }
  #section-compras { position: absolute; left: 0; top: 0; }
  @page { margin: 16mm; }
}
```

---

## 8. HTML Structure Rules

- **Single file, no build tools.** All CSS and JS inlined. Only external dependency: Google Fonts `<link>` (Inter).
- **No JavaScript required** for layout or navigation. JS only for: localStorage checkbox persistence, scroll-based nav activation.
- **CSS custom properties** for all colour tokens in `:root`.
- **Semantic HTML:** `<header>`, `<section>`, `<article>`, `<nav>`, `<ul>/<li>`.
- **Dark mode:** `@media (prefers-color-scheme: dark)` only. Last block in `<style>` before `</style>`.
- **File naming:** `YYYY-MM-DD.html` for session reports, `YYYY-WNN.html` for weekly plans.
- **Never write to `public/`.** All HTML pages are private documents — `private/data/sessions/` or `private/data/plans/` only.

---

## 9. Assets Convention

### Session report images

Images referenced in a session report live in a folder alongside the HTML file:

```
private/data/sessions/
  YYYY-MM-DD.md
  YYYY-MM-DD.html
  assets/
    YYYY-MM-DD/
      IMG_0001.jpeg
      IMG_0002.jpeg
```

The HTML uses relative paths: `assets/YYYY-MM-DD/IMG_0001.jpeg`.

This makes each session self-contained — HTML + assets folder can be moved or shared together without breaking images.

---

## 10. Versioning

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-18 | Extracted from `template-spec.md` v1.3 (plan week). First unified design system covering both weekly plan and session report pages. |

When making changes: update the version table, update all dependent specs (`template-spec.md`, `session-report-spec.md`), note which components are affected.
