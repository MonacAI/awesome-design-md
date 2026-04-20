# VesselWise Design System

A VesselWise-specific extension of the MonacAI Design System. Governs all UI and document output for the VesselWise platform — a yacht quality standards library and survey dashboard. Inherits the full MonacAI base (DESIGN.md) and overrides where VesselWise brand identity, maritime inspection workflows, and dashboard-specific components require it.

**Tagline:** FOR EVERY VESSEL

---

## 1. Visual Theme & Atmosphere

VesselWise communicates institutional authority, technical precision, and maritime expertise. The platform serves two primary surfaces: a **Standards Library** for document review and quality specification, and a **Survey Dashboard** for live inspection data, condition assessments, and photographic evidence.

**Design registers:**
- **Light mode** — Standards Library, document view, printed reports. Clean, authoritative, optimized for reading.
- **Dark mode** — Survey Dashboard, inspection interface, night-use data display. High-contrast, data-forward, optimized for rapid condition assessment.

**Key characteristics:**
- VW Dark (`#232E33`) as the primary brand surface — used for headers, hero sections, and document anchors
- VW Teal (`#35464A`) as the secondary brand surface — section accents, active states, icon fills
- Maritime Blue (`#1c69d4` / `#0653b6`) as interactive color — all buttons, links, and actionable UI
- Inter for all headings and body text — negative tracking at display sizes
- D-DIN for standard section codes and classification headers — e.g. `VW-STD-001`, `VW-HULL-003`
- IBM Plex Mono for all inspection metrics, version numbers, and data fields
- DM Sans as fallback display font per VesselWise branding guidance
- Condition rating system anchored to five semantic colors (Excellent → Critical)
- `"tnum"` tabular numerals mandatory on all numeric inspection data

---

## 2. Color Palette & Roles

### CSS Custom Properties

```css
:root {
  /* VesselWise Primary Brand */
  --vw-dark:               #232E33;   /* Primary brand dark — headers, nav, hero fills */
  --vw-teal:               #35464A;   /* Secondary brand — left icon, "VESSEL" word, section accents */
  --vw-dark-hover:         #1a2228;   /* VW Dark hover state (5% darker) */
  --vw-teal-hover:         #2a383b;   /* VW Teal hover state */
  --vw-dark-rgb:           35,46,51;  /* For rgba() use */
  --vw-teal-rgb:           53,70,74;  /* For rgba() use */

  /* Maritime Blue — Interactive (inherited from MonacAI) */
  --vw-blue:               #1c69d4;   /* Primary interactive — buttons, links */
  --vw-blue-deep:          #0653b6;   /* Focus, active states */
  --vw-blue-bright:        #2997ff;   /* Links on dark backgrounds */

  /* Condition Rating System */
  --condition-1:           #24a148;   /* 1 - Excellent (IBM Green 50) */
  --condition-2:           #0f62fe;   /* 2 - Good (IBM Blue 60) */
  --condition-3:           #f1c21b;   /* 3 - Fair (IBM Yellow 30) */
  --condition-3-text:      #946300;   /* 3 - Fair text (accessible amber on white) */
  --condition-4:           #C8520A;   /* 4 - Poor (IBM Orange) */
  --condition-5:           #da1e28;   /* 5 - Critical (IBM Red 60) */

  /* Neutral Scale — Light Mode */
  --vw-text-primary:       #232E33;   /* VW Dark as heading text — brand-consistent */
  --vw-text-secondary:     #525252;   /* Descriptions, helper text */
  --vw-text-tertiary:      #6f6f6f;   /* Placeholders, metadata */
  --vw-text-caption:       #757575;   /* Timestamps, captions */
  --vw-surface-page:       #ffffff;   /* Page background */
  --vw-surface-card:       #f5f5f7;   /* Card fills, row alternates */
  --vw-surface-elevated:   #f4f4f4;   /* Panels, section alternates */
  --vw-border-default:     #dce4e8;   /* Standard borders (teal-tinted Stripe technique) */
  --vw-border-subtle:      #ebebeb;   /* Subtle separators */

  /* Neutral Scale — Dark Mode (Dashboard) */
  --vw-dark-bg:            #0d1214;   /* Deepest canvas — VW Dark lineage */
  --vw-dark-surface-1:     #151c1f;   /* Sidebar, panel backgrounds */
  --vw-dark-surface-2:     #1e2729;   /* Elevated surfaces, cards */
  --vw-dark-surface-3:     #28343a;   /* Hover states */
  --vw-dark-surface-accent:#232E33;   /* Brand-exact dark surface for accent panels */
  --vw-dark-text-primary:  #f0f4f5;   /* Near-white, slight teal warmth */
  --vw-dark-text-secondary:#b8c4c8;   /* Cool blue-grey */
  --vw-dark-text-tertiary: #6e7e84;   /* Muted */
  --vw-dark-border:        rgba(53,70,74,0.35);  /* VW Teal-tinted card borders */

  /* Semantic Status (shared with MonacAI) */
  --status-critical:       #da1e28;
  --status-poor:           #C8520A;
  --status-warning:        #f1c21b;
  --status-good:           #0f62fe;
  --status-excellent:      #24a148;

  /* Footer & Attribution */
  --vw-footer-text:        #888888;   /* "Powered by VesselWise" — monochrome grey */

  /* Shadow Colors */
  --vw-shadow-brand:       rgba(35,46,51,0.25);  /* VW Dark-tinted primary shadow */
  --vw-shadow-neutral:     rgba(0,0,0,0.10);
  --vw-shadow-ambient:     rgba(0,0,0,0.06);
}
```

### Condition Rating Color Reference

| Rating | Label | Color | Hex | Background Tint |
|--------|-------|-------|-----|-----------------|
| 1 | Excellent | Green | `#24a148` | `rgba(36,161,72,0.12)` |
| 2 | Good | Blue | `#0f62fe` | `rgba(15,98,254,0.12)` |
| 3 | Fair | Amber | `#f1c21b` (text: `#946300`) | `rgba(241,194,27,0.15)` |
| 4 | Poor | Orange | `#C8520A` | `rgba(200,82,10,0.12)` |
| 5 | Critical | Red | `#da1e28` | `rgba(218,30,40,0.12)` |

**Accessibility note:** Condition 3 (Fair) must display `#946300` as text color on light backgrounds — never `#f1c21b` directly on white (fails WCAG AA). On dark backgrounds, use `#f1c21b` directly.

---

## 3. Typography Rules

### Font Families

| Role | Font | Source | Fallbacks |
|------|------|--------|-----------|
| Display & Body | Inter | Google Fonts (free) | DM Sans, SF Pro Display, Arial, sans-serif |
| Display Fallback | DM Sans | Google Fonts (free) | Helvetica Neue, Arial, sans-serif |
| Standard Codes / Classification | D-DIN | Free download | Barlow Condensed, Arial Narrow, sans-serif |
| Inspection Metrics & Data | IBM Plex Mono | Google Fonts (free) | SFMono-Regular, Menlo, Courier New, monospace |

> D-DIN is used for standard section codes (e.g. `VW-STD-001`, `VW-HULL-003`) and classification headers. IBM Plex Mono is used for all numeric data: condition scores, version numbers, inspection field values.

### Type Hierarchy

| Role | Font | Size | Weight | Line Height | Letter Spacing | Notes |
|------|------|------|--------|-------------|----------------|-------|
| Display Hero | Inter | 56px | 600 | 1.07 | -1.4px | Platform landing, report covers |
| Display Large | Inter | 48px | 600 | 1.15 | -0.96px | Section hero headings |
| Section Heading | Inter | 32px | 600 | 1.25 | -0.64px | Standards Library section titles |
| Sub-heading | Inter | 24px | 600 | 1.33 | -0.48px | Document group headings |
| Card Title | Inter | 20px | 600 | 1.40 | -0.24px | Standard document cards, finding cards |
| Body Large | Inter | 18px | 400 | 1.56 | normal | Introductions, standard descriptions |
| Body | Inter | 16px | 400 | 1.50 | normal | Checklist items, finding text, form labels |
| Body Emphasis | Inter | 16px | 600 | 1.50 | normal | Emphasized labels, field names |
| Button | Inter | 14px | 500 | 1.43 | normal | All interactive controls |
| Caption | Inter | 12px | 400 | 1.33 | 0.32px | Metadata, photo captions, timestamps |
| Micro | Inter | 10px | 400 | 1.47 | -0.08px | Legal footers, watermark text |
| Standard Code | D-DIN | 13px | 700 | 1.00 | 1.0px | `VW-STD-001` — uppercase, classification codes |
| Classification Header | D-DIN | 14–16px | 700 | 1.25 | 0.8px | Section headers (HULL, ELECTRICAL, etc.) |
| Version / Build Tag | IBM Plex Mono | 11px | 400 | 1.29 | 0.16px | `v2.1.0`, `Rev 4`, approval builds |
| Metric Display | IBM Plex Mono | 48px | 300 | 1.00 | 0 | Large condition scores, KPI values |
| Metric Value | IBM Plex Mono | 24px | 400 | 1.17 | 0 | Dashboard metrics, inspection scores |
| Data Table | IBM Plex Mono | 14px | 400 | 1.29 | 0.16px | Inspection data tables, numeric fields |

### OpenType Features

- **`"tnum"`** — mandatory on ALL numeric data: condition ratings, version numbers, inspection counts, survey dates displayed in tables
- **`"liga"`** — enabled on Inter and IBM Plex Mono
- **`"case"`** — enabled on D-DIN classification headers

### Principles

- Negative tracking at display sizes (Inter): -1.4px at 56px, -0.96px at 48px, -0.64px at 32px, normal at 16px and below
- D-DIN uppercase labels use **positive** tracking (1.0px) — the contrast between tight Inter headings and wide D-DIN codes creates clear visual register separation
- When IBM Plex Mono appears on dark dashboard surfaces, apply `color: var(--vw-blue-bright)` to distinguish data from descriptive text
- DM Sans is used only as Inter's fallback — never simultaneously on the same surface

---

## 4. Component Specifications

### 4a. Buttons

**Primary (Maritime Blue)**
- Background: `var(--vw-blue)` (`#1c69d4`)
- Text: `#ffffff`
- Padding: 10px 20px
- Radius: 6px
- Font: Inter 14px weight 500
- Hover: `var(--vw-blue-deep)` (`#0653b6`)
- Focus: `2px solid var(--vw-blue-deep)` outline, 2px offset

**Brand Dark (VesselWise Primary)**
- Background: `var(--vw-dark)` (`#232E33`)
- Text: `#ffffff`
- Padding: 10px 20px
- Radius: 6px
- Hover: `var(--vw-dark-hover)` (`#1a2228`)
- Use: Primary CTA on white backgrounds, "Submit Inspection", "Approve Standard"

**Secondary (Outlined)**
- Background: transparent
- Text: `var(--vw-blue)` (`#1c69d4`)
- Border: `1px solid var(--vw-border-default)`
- Hover: `rgba(28,105,212,0.05)` background tint

**Ghost**
- Background: transparent
- Text: `var(--vw-blue)`
- No border
- Hover: `var(--vw-surface-card)`

**Danger**
- Background: `var(--status-critical)` (`#da1e28`)
- Text: `#ffffff`
- Hover: `#b81921`
- Use: Flag critical, reject inspection

---

### 4b. Standards Library — Document Cards

Document cards present individual VesselWise quality standards. Each card represents one standard document.

```
┌─────────────────────────────────────────────────┐
│ [VW-STD-001]  [v2.1]  [● APPROVED]              │
│                                                   │
│ Hull Structural Integrity Standard               │
│ Applies to: Fibreglass, Steel, Aluminium         │
│                                                   │
│ Last revised: 12 Mar 2026  · 8 sections          │
│                                         [View →] │
└─────────────────────────────────────────────────┘
```

**Light Mode Card**
- Background: `#ffffff`
- Border: shadow-as-border — `rgba(0,0,0,0.08) 0px 0px 0px 1px`
- Shadow: `var(--vw-shadow-brand) 0px 20px 35px -20px, var(--vw-shadow-neutral) 0px 12px 24px -12px`
- Radius: 8px
- Padding: 20px 24px

**Standard Code Badge**
- Font: D-DIN, 13px, weight 700, uppercase, 1.0px tracking
- Background: `rgba(35,46,51,0.08)` (VW Dark tint)
- Text: `var(--vw-dark)` (`#232E33`)
- Padding: 3px 8px
- Radius: 4px

**Version Badge**
- Font: IBM Plex Mono, 11px, weight 400
- Background: `rgba(28,105,212,0.10)`
- Text: `#0653b6`
- Padding: 3px 7px
- Radius: 4px

**Approval Status Indicators**

| Status | Background | Text | Dot Color |
|--------|-----------|------|-----------|
| Approved | `rgba(36,161,72,0.12)` | `#24a148` | `#24a148` |
| Under Review | `rgba(241,194,27,0.15)` | `#946300` | `#f1c21b` |
| Draft | `rgba(0,0,0,0.06)` | `#525252` | `#6f6f6f` |
| Superseded | `rgba(218,30,40,0.10)` | `#da1e28` | `#da1e28` |

All approval badges: Inter 12px weight 500, 24px pill radius, 4px 10px padding. Prepend with a 6px dot `●` at matching color.

---

### 4c. Survey Dashboard — Condition Rating Badges

The five-point condition scale is the core semantic unit of the dashboard. Badges must be visually distinct, never rely on color alone (always include the numeral), and support both compact (number-only) and full (number + label) variants.

**Full Badge**
- Layout: `[1] Excellent`
- Padding: 5px 12px
- Radius: 24px (pill)
- Font: Inter 13px weight 600
- Number: IBM Plex Mono 13px weight 600, `"tnum"`, same color

**Compact Badge (table/card use)**
- Layout: `[1]`
- Width: 28px, Height: 28px
- Radius: 6px
- Font: IBM Plex Mono 14px weight 700, `"tnum"`
- Centered

| Rating | Label | Badge BG | Badge Text |
|--------|-------|----------|------------|
| 1 | Excellent | `rgba(36,161,72,0.12)` | `#24a148` |
| 2 | Good | `rgba(15,98,254,0.12)` | `#0f62fe` |
| 3 | Fair | `rgba(241,194,27,0.15)` | `#946300` |
| 4 | Poor | `rgba(200,82,10,0.12)` | `#C8520A` |
| 5 | Critical | `rgba(218,30,40,0.12)` | `#da1e28` |

**Dark mode overrides:**
- Rating 3 text: `#f1c21b` (safe on dark surface)
- All other text colors: use as-is (sufficient contrast on `#1e2729`)

---

### 4d. Survey Dashboard — Finding Cards

A finding card represents a single inspection observation linked to a VesselWise standard.

```
┌────────────────────────────────────────────────────┐
│  [4 Poor]   VW-HULL-003                            │
│                                                     │
│  Stress cracking observed at port side chine       │
│  weld joint, approx 340mm forward of frame 12.     │
│                                                     │
│  📷 3 photos  · Surveyor: J. Whitfield             │
│  Located: Hull — Frame 10–14, Port              │
│                             [View Evidence →]      │
└────────────────────────────────────────────────────┘
```

**Light Mode**
- Background: `#ffffff`
- Left accent bar: 3px solid, color matches condition rating
- Border: `rgba(0,0,0,0.07) 0px 0px 0px 1px`
- Shadow: ambient only — `rgba(0,0,0,0.06) 0px 3px 6px`
- Radius: 8px
- Padding: 16px 20px

**Dark Mode**
- Background: `var(--vw-dark-surface-2)` (`#1e2729`)
- Left accent bar: same condition color, full opacity
- Border: `1px solid var(--vw-dark-border)`
- No shadow

**Finding Card Typography**
- Standard code: D-DIN 13px weight 700, uppercase, 1.0px tracking, `var(--vw-teal)` on light / `#5a7c82` on dark
- Finding title: Inter 16px weight 600, `var(--vw-text-primary)` / `var(--vw-dark-text-primary)`
- Finding body: Inter 15px weight 400, `var(--vw-text-secondary)`
- Metadata row: Inter 12px weight 400, `var(--vw-text-caption)`

---

### 4e. Survey Dashboard — Photo Evidence Containers

Photo evidence containers display inspection photographs inline with findings.

**Thumbnail Grid**
- Layout: flex row, gap 8px
- Each thumbnail: 80×80px (compact) or 120×120px (expanded)
- Radius: 6px
- Object-fit: cover
- Overlay on hover: `rgba(35,46,51,0.4)` with fullscreen icon (`⤢`) centered in Inter 18px white

**Lightbox / Full Evidence Panel**
- Background: `rgba(13,18,20,0.92)` (near-black modal scrim)
- Image: centered, max 90vw × 80vh, radius 4px
- Caption: Inter 13px weight 400, `#b8c4c8`, below image, centered
- Navigation arrows: 36×36px, `rgba(255,255,255,0.12)` bg, white chevron
- Close: top-right, `×` at 24px Inter, `var(--vw-dark-text-secondary)`

**Photo Count Badge**
- `📷 N photos` — Inter 12px weight 500, `var(--vw-text-caption)`
- Use the camera icon as a Unicode glyph or SVG, never as an IMG element inline

---

### 4f. Inspection Forms — Checklist Items

Checklist items represent individual inspection line items within a VesselWise standard section.

```
[✓] Bilge pump operational and accessible         [1 Excellent ▾]
[✗] Seacocks below waterline — full movement      [5 Critical  ▾]
[–] Engine room ventilation adequate              [Not Assessed]
```

**Row Structure**
- Height: 44px minimum (touch target)
- Padding: 10px 16px
- Border-bottom: `0.5px solid var(--vw-border-subtle)`
- Hover: `var(--vw-surface-card)` background
- Font: Inter 15px weight 400

**Checkbox / Status Icon**
- Pass `[✓]`: `#24a148`, 18×18px, radius 4px
- Fail `[✗]`: `#da1e28`, 18×18px, radius 4px
- N/A `[–]`: `#6f6f6f`, 18×18px, radius 4px
- Pending `[○]`: `var(--vw-border-default)` stroke, no fill

**Pass/Fail Indicator Row (section summary)**
- Layout: `[✓ 18 Pass] [✗ 3 Fail] [– 2 N/A]`
- Font: Inter 13px weight 600
- Pass: `#24a148` | Fail: `#da1e28` | N/A: `#6f6f6f`
- Background: `var(--vw-surface-elevated)`, padding 10px 16px, radius 6px

**Inline Rating Selector**
- Default: condition rating badge showing current value
- On interaction: dropdown list of all 5 ratings with color-coded rows
- Font: Inter 13px weight 500

---

### 4g. Tables

**Standards Library Index Table**
- Header row: `var(--vw-dark)` background, `#ffffff` text
- Header font: Inter 12px weight 600, uppercase, 0.32px tracking
- Code column: D-DIN 13px weight 700, 1.0px tracking
- Body text: Inter 14px weight 400
- Numeric values: IBM Plex Mono 14px weight 400, `"tnum"`
- Alternating rows: `#ffffff` / `var(--vw-surface-elevated)`
- Border: `0.5px solid var(--vw-border-subtle)`
- Row padding: 11px 16px
- Hover: `rgba(35,46,51,0.04)` background tint

**Inspection Data Table**
- Header row: `var(--vw-teal)` background, `#ffffff` text
- Body: IBM Plex Mono 14px for all measurement/score columns
- Condition rating cells: show compact badge (28×28px)
- Row height: 44px minimum

---

### 4h. Navigation (Dashboard)

**Top Bar — Light Mode**
- Background: `#ffffff` with `backdrop-filter: saturate(180%) blur(20px)`
- Height: 56px
- Left: VesselWise logo mark + "VesselWise" wordmark in Inter 15px weight 600
- Links: Inter 14px weight 500, `var(--vw-text-primary)`, active state with `var(--vw-teal)` underline 2px
- Right: User avatar, notifications, primary CTA button

**Top Bar — Dark Mode**
- Background: `rgba(13,18,20,0.88)` with `backdrop-filter: blur(20px)`
- Logo: reversed white version
- Links: `var(--vw-dark-text-secondary)`, hover `var(--vw-dark-text-primary)`

**Sidebar — Dark Mode (Dashboard)**
- Background: `var(--vw-dark-surface-1)` (`#151c1f`)
- Width: 240px
- Section headers: D-DIN 11px weight 700, uppercase, 1.5px tracking, `var(--vw-dark-text-tertiary)`
- Nav items: Inter 14px weight 400, `var(--vw-dark-text-secondary)`
- Active item: background `var(--vw-dark-surface-3)`, left border 3px `var(--vw-teal)`, text `var(--vw-dark-text-primary)`
- Standard code pills in nav: IBM Plex Mono 11px, `rgba(53,70,74,0.5)` bg

---

### 4i. Metric / KPI Cards

**Light Mode KPI Card**
- Background: `#ffffff`
- Shadow: `var(--vw-shadow-brand) 0px 20px 35px -20px, var(--vw-shadow-neutral) 0px 12px 24px -12px`
- Radius: 8px
- Padding: 20px 24px
- Metric value: IBM Plex Mono 48px weight 300, `"tnum"`, `var(--vw-dark)` (`#232E33`)
- Label: Inter 12px weight 500, uppercase, 0.32px tracking, `var(--vw-text-caption)`
- Delta: `var(--status-excellent)` (up) / `var(--status-critical)` (down) with arrow
- Subtext: Inter 12px weight 400, `var(--vw-text-tertiary)`

**Dark Mode KPI Card**
- Background: `var(--vw-dark-surface-2)` (`#1e2729`)
- Border: `1px solid var(--vw-dark-border)`
- Radius: 8px
- Metric value: IBM Plex Mono 48px weight 300, `"tnum"`, `var(--vw-blue-bright)` (`#2997ff`)
- Label: Inter 12px weight 500, uppercase, 0.32px tracking, `var(--vw-dark-text-tertiary)`

---

## 5. Layout Principles

### Spacing System (8px base — IBM Carbon)

| Token | Value | Use |
|-------|-------|-----|
| `--vw-space-1` | 2px | Micro adjustments, icon gaps |
| `--vw-space-2` | 4px | Badge internal gaps |
| `--vw-space-3` | 8px | Base unit, tight padding |
| `--vw-space-4` | 12px | Compact card padding |
| `--vw-space-5` | 16px | Standard component gaps |
| `--vw-space-6` | 24px | Card padding, section sub-gaps |
| `--vw-space-7` | 32px | Section gaps |
| `--vw-space-8` | 48px | Major transitions |
| `--vw-space-9` | 64px | Hero padding |

### Dashboard Grid

- 12-column grid
- Max content width: 1280px, centered
- Column gutters: 24px (desktop), 16px (tablet)
- Page margins: 32px (desktop), 16px (mobile)
- Sidebar: 240px fixed (desktop), collapsible overlay (tablet/mobile)

### Standards Library Layout

- Two-column browse: 320px filter/nav column + main content flex
- Document card grid: 3-column (desktop), 2-column (tablet), 1-column (mobile)
- Document detail: single-column max-width 800px, centered, generous vertical rhythm

### Border Radius Scale

| Token | Value | Use |
|-------|-------|-----|
| `--vw-radius-none` | 0px | Document table cells, print contexts |
| `--vw-radius-sm` | 4px | Badges, code chips, thumbnail overlays |
| `--vw-radius-md` | 6px | Buttons, inputs, compact containers |
| `--vw-radius-lg` | 8px | Cards, panels, modals |
| `--vw-radius-xl` | 12px | Featured cards, photo containers |
| `--vw-radius-pill` | 24px | Condition badges, status tags |

---

## 6. Depth & Elevation

| Level | Treatment | Use |
|-------|-----------|-----|
| Flat (Level 0) | No shadow, `var(--vw-surface-page)` | Default page surface |
| Surface (Level 1) | Background shift to `var(--vw-surface-elevated)` | Alternating sections, zebra rows |
| Ambient (Level 2) | `rgba(0,0,0,0.06) 0px 3px 6px` | Finding cards, subtle lift |
| Elevated (Level 3) | `var(--vw-shadow-brand) 0px 20px 35px -20px, var(--vw-shadow-neutral) 0px 12px 24px -12px` | Document cards, KPI cards, dropdowns |
| Floating (Level 4) | `var(--vw-shadow-brand) 0px 30px 45px -20px, var(--vw-shadow-neutral) 0px 18px 36px -18px` | Modals, lightbox panels |
| Glass (Nav) | `backdrop-filter: saturate(180%) blur(20px)` on translucent bg | Sticky top navigation |
| Focus | `2px solid var(--vw-blue-deep)` outline, 2px offset | Keyboard focus ring |

**Shadow philosophy:** VesselWise shadows use VW Dark-tinted base (`rgba(35,46,51,0.25)`) paired with a neutral close layer. The dark teal tint is subtly warmer and more maritime than MonacAI's pure navy — connecting elevation to the brand's coastal character.

**Dark mode:** No shadows. Depth through luminance stepping: `#0d1214` → `#151c1f` → `#1e2729` → `#28343a`. Following Linear's approach.

---

## 7. "Powered by VesselWise" Footer Specification

This component appears on every WOSA survey report generated through the VesselWise platform.

### Layout

```
CONFIDENTIAL               Page X of Y          Powered by VesselWise [icon]
(left-aligned)              (centered)              (right-aligned)
```

### Specifications

- **Full footer container height:** 20pt minimum
- **Text font:** Inter Regular, **7pt**, color `#888888`
- **"VesselWise" text:** Inter Medium (weight 500), **7pt**, color `#888888`
- **Icon mark:** VesselWise icon at **8–10pt height**, rendered in `#888888` (monochrome — no brand colors in footer)
- **Minimum width** of the "Powered by VesselWise" element: 15mm
- **Asset:** Use `assets/VesselWise_Watermark.png` or SVG icon recolored to `#888888` at this scale
- **No brand colors** in footer — strictly monochrome grey throughout
- **Spacing:** 4pt gap between "Powered by VesselWise" text and icon mark
- **Alignment:** Text and icon baseline-aligned

### CSS / HTML Implementation

```css
.vw-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-family: 'Inter', 'DM Sans', Arial, sans-serif;
  font-size: 7pt;
  font-weight: 400;
  color: #888888;
  min-height: 20pt;
}

.vw-footer__powered {
  display: flex;
  align-items: center;
  gap: 4pt;
  min-width: 15mm;
}

.vw-footer__powered strong {
  font-weight: 500;
}

.vw-footer__icon {
  height: 9pt;   /* within 8–10pt range */
  width: auto;
  opacity: 1;    /* already grey in watermark asset */
  filter: grayscale(1) brightness(0.55);  /* if using full-color source */
}
```

---

## 8. Responsive Behavior

### Breakpoints

| Name | Width | Key Changes |
|------|-------|-------------|
| Mobile | <640px | Single column, stacked finding cards, collapsed sidebar, 32px display |
| Tablet | 640–1024px | 2-column card grid, sidebar as overlay drawer |
| Desktop | 1024–1280px | Full 3-column layout, 240px sidebar visible |
| Large Desktop | >1280px | Centered 1280px max-width, generous margins |

### Touch Targets
- Minimum interactive height: 44px
- Checklist row height: 44px minimum
- Condition rating selector: 44px touch area
- Navigation sidebar items: 44px row height

### Collapsing Strategy
- Dashboard sidebar: 240px fixed → overlay drawer on tablet → bottom tab bar on mobile
- Finding card grid: 3-col → 2-col → 1-col
- Standards Library grid: 3-col → 2-col → 1-col
- Metric KPI cards: 4-col → 2-col → 1-col vertical stack
- Data tables: horizontal scroll on mobile, condition badge column sticky
- Document detail view: 800px max → full width with 16px margins

### Typography Scaling
- Display Hero: 56px → 36px on mobile
- Section Heading: 32px → 24px on mobile
- Body: 16px maintained at all sizes
- Metric Display (IBM Plex Mono): 48px → 32px on mobile

---

## 9. Agent Prompt Guide

### Quick Color Reference

```
Brand primary dark:    #232E33  (VW Dark — headers, nav, document anchors)
Brand teal:            #35464A  (VW Teal — section accents, icon left half)
Interactive blue:      #1c69d4  (Maritime Blue — buttons, links)
Interactive deep:      #0653b6  (Focus, active)
Interactive bright:    #2997ff  (Links on dark bg)

Heading text (light):  #232E33  (VW Dark as heading text)
Body text:             #525252
Caption / meta:        #757575
Border:                #dce4e8

Dark background:       #0d1214
Dark surface card:     #1e2729
Dark text primary:     #f0f4f5
Dark text secondary:   #b8c4c8

Condition 1 Excellent: #24a148 (green)
Condition 2 Good:      #0f62fe (blue)
Condition 3 Fair:      #946300 (amber text) / #f1c21b (amber swatch)
Condition 4 Poor:      #C8520A (orange)
Condition 5 Critical:  #da1e28 (red)

Footer grey:           #888888
```

### Example Component Prompts

**Standards Library document card:**
"Create a document card on white background. Shadow: rgba(35,46,51,0.25) 0px 20px 35px -20px, rgba(0,0,0,0.1) 0px 12px 24px -12px. 8px radius. 20px 24px padding. Top row: D-DIN 13px 700 uppercase 1.0px tracking code badge (rgba(35,46,51,0.08) bg, #232E33 text, 4px radius), IBM Plex Mono 11px version badge (rgba(28,105,212,0.10) bg, #0653b6 text), and approval status pill (Inter 12px 500, 24px radius, 4px 10px). Card title: Inter 20px weight 600, letter-spacing -0.24px, color #232E33. Sub-line: Inter 14px 400 color #525252. Footer row: Inter 12px 400 color #757575."

**Survey finding card (condition 4 Poor):**
"Create a finding card: white background, left accent bar 3px solid #C8520A, shadow rgba(0,0,0,0.06) 0px 3px 6px, 8px radius, 16px 20px padding. Condition badge: rgba(200,82,10,0.12) bg, #C8520A text, Inter 13px 600, 24px radius. Standard code: D-DIN 13px 700 uppercase 1.0px tracking color #35464A. Finding title: Inter 16px 600 color #232E33. Body: Inter 15px 400 color #525252. Meta row: Inter 12px 400 color #757575."

**Condition rating badge (full set):**
"Create five condition rating pills. Each: Inter 13px 600, 24px radius, 5px 12px padding, numeral in IBM Plex Mono 13px 600 'tnum'. Backgrounds and text: 1=rgba(36,161,72,0.12)/#24a148, 2=rgba(15,98,254,0.12)/#0f62fe, 3=rgba(241,194,27,0.15)/#946300, 4=rgba(200,82,10,0.12)/#C8520A, 5=rgba(218,30,40,0.12)/#da1e28."

**Dark mode dashboard panel:**
"Create a dashboard panel: #1e2729 background, 8px radius, 1px solid rgba(53,70,74,0.35) border. Section header: D-DIN 11px 700 uppercase 1.5px tracking, color #6e7e84. Panel title: Inter 20px 600, color #f0f4f5. Metric value: IBM Plex Mono 48px 300 'tnum', color #2997ff. Label: Inter 12px 500 uppercase 0.32px tracking, color #6e7e84. Condition badge on dark: full opacity colors (see rating table)."

**Inspection form checklist:**
"Build a checklist section: each row 44px height, Inter 15px 400 text color #232E33, padding 10px 16px, border-bottom 0.5px solid #ebebeb, hover #f5f5f7. Status icons 18×18px radius 4px: pass #24a148, fail #da1e28, na #6f6f6f. Right side: inline condition rating selector badge. Summary bar below: rgba(244,244,244,1.0) background, Inter 13px 600 — Pass in #24a148, Fail in #da1e28, N/A in #6f6f6f."

**KPI metric card (dark mode):**
"Metric card: #1e2729 bg, 8px radius, 1px solid rgba(53,70,74,0.35). Metric: IBM Plex Mono 48px 300 'tnum' color #2997ff. Label: Inter 12px 500 uppercase 0.32px tracking color #6e7e84. Delta: arrow + IBM Plex Mono 14px 'tnum', up=#24a148, down=#da1e28."

**"Powered by VesselWise" footer:**
"Footer row: flex space-between. Left: 'CONFIDENTIAL' 7pt Inter 400 #888888. Center: 'Page X of Y' 7pt Inter 400 #888888. Right: 'Powered by ' 7pt Inter 400 #888888 + 'VesselWise' 7pt Inter 500 #888888 + VesselWise icon at 9pt height, greyscale, min-width 15mm."

### Iteration Guide

1. Heading color on light backgrounds is always `#232E33` (VW Dark) — never pure black or monacai navy
2. All numeric data (scores, versions, counts, measurements) use IBM Plex Mono with `"tnum"` — no exceptions
3. Standard codes and classification labels use D-DIN uppercase with 1.0px tracking — always
4. Interactive elements (buttons, links, focus rings) use Maritime Blue (`#1c69d4`/`#0653b6`) — not VW brand colors
5. Condition ratings are always displayed with BOTH a numeral and a label (compact badge minimum shows numeral; full badge shows numeral + label)
6. Finding cards always carry a colored left accent bar matching the condition rating — never just a badge
7. Shadow formula: `rgba(35,46,51,0.25) 0px Y1 B1 -S1, rgba(0,0,0,0.1) 0px Y2 B2 -S2` (VW Dark-tinted)
8. Dark mode uses luminance stepping: `#0d1214` → `#151c1f` → `#1e2729` → `#28343a` — no shadows
9. "Powered by VesselWise" footer: always 7pt Inter, always `#888888`, always greyscale icon — no exceptions
10. VW Dark (`#232E33`) and VW Teal (`#35464A`) are brand surfaces only — never use as button/link interactive colors
11. Approval status badges use a 6px dot `●` prepended — color + label, never color alone
12. D-DIN uppercase classification headers use `"case"` OpenType feature when available
13. Photo evidence: thumbnails are 80–120px square, radius 6px, hover shows `rgba(35,46,51,0.4)` overlay
14. Footer component is the highest-fidelity output requirement — test at actual 7pt before shipping
