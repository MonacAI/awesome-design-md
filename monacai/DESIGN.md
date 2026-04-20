# MonacAI Design System

A unified design language for all MonacAI projects. Built by combining the strongest elements from Stripe, Apple, IBM, Linear, BMW, Vercel, and SpaceX design systems -- adapted for maritime quality standards, KPI dashboards, and professional survey documents.

## 1. Visual Theme & Atmosphere

MonacAI's design communicates precision, maritime authority, and premium professionalism. The system operates in two registers: a **light mode** for documents, standards, and executive dashboards, and a **dark mode** for technical monitoring, night-mode interfaces, and immersive displays.

The design philosophy is "content as hero" -- interfaces and documents retreat behind the data and findings they present. No decorative chrome, no gratuitous animation, no visual noise. Every element earns its place through function.

**Key Characteristics:**
- Inter as the universal typeface with negative letter-spacing at display sizes (inspired by Apple/Stripe)
- Maritime blue accent palette derived from BMW (`#1c69d4`) and Apple (`#0071e3`)
- D-DIN for technical labels and classification headers (SpaceX -- free, DIN-heritage)
- IBM Plex Mono for data, metrics, and code (open-source)
- Multi-layer shadow system adapted from Stripe's blue-tinted approach
- `"tnum"` tabular numerals for all financial and metric data (Stripe)
- CSS custom property architecture for multi-project theming (BMW `--site-context-*` pattern)
- 8px spacing grid with strict adherence (IBM Carbon)

## 2. Color Palette & Roles

### CSS Custom Properties

All colors are defined as CSS custom properties for easy theming across projects:

```css
:root {
  /* Primary Brand */
  --monacai-navy:          #0A2342;   /* Deepest brand color, footer, immersive sections */
  --monacai-blue:          #1c69d4;   /* Primary interactive accent (from BMW) */
  --monacai-blue-deep:     #0653b6;   /* Focus states, active indicators (from BMW) */
  --monacai-blue-bright:   #2997ff;   /* Links on dark backgrounds (from Apple) */
  --monacai-blue-light:    #0071e3;   /* Secondary interactive (from Apple) */

  /* WOSA / VesselWise Brand Integration */
  --wosa-red:              #A61B2B;   /* WOSA brand accent -- document headers, links */
  --wosa-teal:             #1A6B6E;   /* WOSA section headers, subsection headings */
  --vw-dark:               #232E33;   /* VesselWise dark -- right side of icon */
  --vw-teal:               #35464A;   /* VesselWise teal -- left side of icon */

  /* Neutral Scale (Light Mode) */
  --text-primary:          #0A2342;   /* Deep navy headings -- not black (Stripe principle) */
  --text-secondary:        #525252;   /* Descriptions, helper text (IBM Gray 70) */
  --text-tertiary:         #6f6f6f;   /* Placeholders, disabled (IBM Gray 60) */
  --text-caption:          #757575;   /* Metadata, timestamps (BMW Meta Gray) */
  --surface-page:          #ffffff;   /* Page background */
  --surface-card:          #f5f5f7;   /* Card fills, alternating rows (Apple Light Gray) */
  --surface-elevated:      #f4f4f4;   /* Elevated panels (IBM Gray 10) */
  --border-default:        #e5edf5;   /* Standard borders (Stripe) */
  --border-subtle:         #ebebeb;   /* Subtle separators (Vercel Gray 100) */

  /* Neutral Scale (Dark Mode) */
  --dark-bg:               #08090a;   /* Deepest canvas (Linear Marketing Black) */
  --dark-surface-1:        #0f1011;   /* Sidebar, panel backgrounds (Linear) */
  --dark-surface-2:        #191a1b;   /* Elevated surfaces, cards (Linear) */
  --dark-surface-3:        #28282c;   /* Hover states (Linear) */
  --dark-text-primary:     #f7f8f8;   /* Near-white text (Linear) */
  --dark-text-secondary:   #d0d6e0;   /* Cool silver-gray (Linear) */
  --dark-text-tertiary:    #8a8f98;   /* Muted gray (Linear) */
  --dark-border:           rgba(255,255,255,0.08);  /* Card borders (Linear) */

  /* Semantic Status Colors (IBM Carbon tokens) */
  --status-error:          #da1e28;   /* Red 60 -- critical findings, danger */
  --status-success:        #24a148;   /* Green 50 -- compliant, positive */
  --status-warning:        #f1c21b;   /* Yellow 30 -- needs attention */
  --status-info:           #0f62fe;   /* Blue 60 -- informational */

  /* Document-Specific */
  --impact-bg:             #FFF8F0;   /* Business impact callout background */
  --impact-border:         #C8520A;   /* Business impact accent bar */
  --impact-text:           #7A3000;   /* Business impact text */

  /* Shadow Colors (Stripe-inspired) */
  --shadow-brand:          rgba(10,35,66,0.25);  /* Navy-tinted primary shadow */
  --shadow-neutral:        rgba(0,0,0,0.1);      /* Secondary shadow layer */
  --shadow-ambient:        rgba(0,0,0,0.06);     /* Subtle ambient lift */
  --shadow-border:         rgba(0,0,0,0.08);     /* Shadow-as-border (Vercel) */
}
```

### Status Color Usage

| Status | Color | Hex | Use |
|--------|-------|-----|-----|
| Critical / Danger | Red | `#da1e28` | Critical findings, failed inspections, error states |
| Warning / Attention | Amber | `#f1c21b` | Observations requiring attention, moderate risk |
| Success / Compliant | Green | `#24a148` | Passed inspections, positive findings, compliant |
| Informational | Blue | `#0f62fe` | Notes, references, informational callouts |
| Priority 1 | Orange | `#C8520A` | Highest priority actions (WOSA documents) |

## 3. Typography Rules

### Font Families

| Role | Font | Source | Fallbacks |
|------|------|--------|-----------|
| Display & Body | Inter | Google Fonts (free) | SF Pro Display, Helvetica Neue, Arial, sans-serif |
| Technical Labels | D-DIN | Free download | Barlow Condensed, Arial Narrow, sans-serif |
| Data & Metrics | IBM Plex Mono | Google Fonts (free) | SFMono-Regular, Menlo, Courier New, monospace |
| Enterprise Alt | IBM Plex Sans | Google Fonts (free) | Helvetica Neue, Arial, sans-serif |

### Hierarchy

| Role | Font | Size | Weight | Line Height | Letter Spacing | Features | Notes |
|------|------|------|--------|-------------|----------------|----------|-------|
| Display Hero | Inter | 56px | 600 | 1.07 | -1.4px | -- | Maximum impact (Apple line-height, Stripe tracking) |
| Display Large | Inter | 48px | 600 | 1.15 | -0.96px | -- | Secondary hero |
| Section Heading | Inter | 32px | 600 | 1.25 | -0.64px | -- | Feature section titles |
| Sub-heading | Inter | 24px | 600 | 1.33 | -0.48px | -- | Card headings, sub-sections |
| Card Title | Inter | 20px | 600 | 1.40 | -0.24px | -- | Card titles (IBM Heading 04 scale) |
| Body Large | Inter | 18px | 400 | 1.56 | normal | -- | Introductions, descriptions |
| Body | Inter | 16px | 400 | 1.50 | normal | -- | Standard reading text |
| Body Emphasis | Inter | 16px | 600 | 1.50 | normal | -- | Emphasized body, labels |
| Button | Inter | 14px | 500 | 1.43 | normal | -- | Buttons, links |
| Caption | Inter | 12px | 400 | 1.33 | 0.32px | -- | Metadata, timestamps (IBM tracking) |
| Micro | Inter | 10px | 400 | 1.47 | -0.08px | -- | Legal text, footnotes |
| Technical Label | D-DIN | 12-14px | 700 | 1.00 | 1.0px | uppercase | Classification headers, section codes |
| Technical Body | D-DIN | 14-16px | 400 | 1.50 | normal | -- | Technical standard body text |
| Metric Display | IBM Plex Mono | 48px | 300 | 1.00 | 0 | tnum | Large KPI numbers |
| Metric Value | IBM Plex Mono | 24px | 400 | 1.17 | 0 | tnum | Dashboard metric values |
| Data Table | IBM Plex Mono | 14px | 400 | 1.29 | 0.16px | tnum | Table numbers, financial data |
| Code | IBM Plex Mono | 14px | 400 | 1.43 | 0.16px | -- | Code blocks, technical content |

### OpenType Features

- **`"tnum"`** (tabular numerals): Mandatory on ALL numeric data -- metric displays, tables, charts, financial figures. Numbers must align vertically in columns.
- **`"liga"`** (ligatures): Enabled on Inter and IBM Plex Mono for tighter glyph combinations.
- **`"cv01"`** (character variant): Optional on Inter for alternate letterforms in display contexts.

### Principles

- **Negative tracking at display sizes**: Letter-spacing tightens proportionally with size (-1.4px at 56px, -0.96px at 48px, -0.64px at 32px, normal at 16px and below). Inspired by Stripe/Apple.
- **Three-weight simplicity**: 400 (body/reading), 500 (UI/interactive), 600 (headings/emphasis). No bold (700) in Inter except for specific document headers. Weight restraint signals confidence.
- **D-DIN for authority**: Technical labels, classification codes, and standard section headers use D-DIN uppercase with positive tracking. The DIN heritage carries engineering credibility.
- **IBM Plex Mono for data**: All numbers in dashboards, reports, and KPI displays use IBM Plex Mono with `"tnum"`. This creates a clear visual register: "when you see monospace, this is data."
- **Micro-tracking at small sizes**: Following IBM Carbon, apply 0.16px at 14px and 0.32px at 12px for readability at compact sizes.

## 4. Component Stylings

### Buttons

**Primary (Maritime Blue)**
- Background: `var(--monacai-blue)` (`#1c69d4`)
- Text: `#ffffff`
- Padding: 10px 20px
- Radius: 6px
- Font: Inter 14px weight 500
- Hover: `var(--monacai-blue-deep)` (`#0653b6`)
- Focus: `2px solid var(--monacai-blue-deep)` outline

**Secondary (Outlined)**
- Background: transparent
- Text: `var(--monacai-blue)` (`#1c69d4`)
- Border: `1px solid var(--border-default)`
- Padding: 10px 20px
- Radius: 6px
- Hover: `rgba(28,105,212,0.05)` background tint

**Ghost**
- Background: transparent
- Text: `var(--monacai-blue)` (`#1c69d4`)
- Border: none
- Hover: `var(--surface-card)` background
- Use: Tertiary actions, inline controls

**Danger**
- Background: `var(--status-error)` (`#da1e28`)
- Text: `#ffffff`
- Hover: `#b81921`

**Dark Mode Primary**
- Background: `var(--monacai-blue-bright)` (`#2997ff`)
- Text: `var(--dark-bg)`
- Hover: `#0071e3`

### Cards & Containers

**Light Mode Card**
- Background: `#ffffff`
- Border: via shadow -- `var(--shadow-border) 0px 0px 0px 1px` (Vercel technique)
- Radius: 8px
- Shadow: `var(--shadow-brand) 0px 20px 35px -20px, var(--shadow-neutral) 0px 12px 24px -12px`
- Hover: shadow intensifies
- Padding: 24px

**Dark Mode Card**
- Background: `var(--dark-surface-2)` (`#191a1b`)
- Border: `1px solid var(--dark-border)` (`rgba(255,255,255,0.08)`)
- Radius: 8px
- Shadow: none (Linear approach -- depth through luminance)
- Padding: 24px

**Metric Card (KPI Display)**
- Background: `#ffffff` or `var(--dark-surface-2)`
- Shadow: full Vercel card stack
- Metric number: IBM Plex Mono, 48px, weight 300, `"tnum"`
- Label: Inter 12px weight 500, uppercase, 0.32px tracking
- Delta indicator: `var(--status-success)` or `var(--status-error)` with arrow

### Badges / Status Tags

**Status Badge**
- Background: status color at 15% opacity
- Text: corresponding status color at full saturation
- Padding: 4px 10px
- Radius: 24px (pill -- IBM exception)
- Font: Inter 12px weight 500

| Status | Background | Text |
|--------|-----------|------|
| Critical | `rgba(218,30,40,0.15)` | `#da1e28` |
| Warning | `rgba(241,194,27,0.15)` | `#946300` |
| Compliant | `rgba(36,161,72,0.15)` | `#24a148` |
| Info | `rgba(15,98,254,0.15)` | `#0f62fe` |

### Tables

**Standard Data Table**
- Header row: `var(--text-primary)` text on `var(--surface-elevated)` background
- Header font: Inter 12px weight 600, uppercase, 0.32px tracking
- Body font: Inter 14px weight 400 (text) or IBM Plex Mono 14px weight 400 `"tnum"` (numbers)
- Alternating rows: `#ffffff` / `var(--surface-elevated)`
- Border: `0.5px solid var(--border-subtle)`
- Row padding: 12px 16px
- Hover: `var(--surface-card)` background

**WOSA Document Table**
- Header row: `var(--wosa-red)` (`#A61B2B`) background, white text
- Header font: Inter SemiBold 9pt
- Body font: Inter Regular 9pt
- Alternating rows: white / `#F5F5F5`
- Border: `0.5px solid #D0D0D0`

### Navigation

**Light Mode**
- Background: `#ffffff` with `backdrop-filter: saturate(180%) blur(20px)` (Apple glass)
- Height: 56px
- Links: Inter 14px weight 500, `var(--text-primary)`
- Active: weight 600, `var(--monacai-blue)` underline
- CTA: Primary button right-aligned

**Dark Mode**
- Background: `rgba(15,16,17,0.85)` with `backdrop-filter: blur(20px)`
- Links: `var(--dark-text-secondary)`, hover to `var(--dark-text-primary)`

## 5. Layout Principles

### Spacing System (8px base -- IBM Carbon)

| Token | Value | Use |
|-------|-------|-----|
| `--space-1` | 2px | Micro adjustments, icon gaps |
| `--space-2` | 4px | Tight element gaps |
| `--space-3` | 8px | Base unit, small padding |
| `--space-4` | 12px | Compact padding |
| `--space-5` | 16px | Standard padding, component gaps |
| `--space-6` | 24px | Card padding, section sub-gaps |
| `--space-7` | 32px | Section gaps |
| `--space-8` | 48px | Major section transitions |
| `--space-9` | 64px | Hero padding |
| `--space-10` | 96px | Maximum section spacing |

### Grid

- 12-column grid for dashboards and web applications
- Max content width: 1200px (desktop), centered with auto margins
- Column gutters: 24px (desktop), 16px (mobile)
- Page margins: 32px (desktop), 16px (mobile)

### Whitespace Philosophy

- **Precision spacing** (Stripe): Every gap is deliberate. Dense data areas have tight spacing; the chrome around them breathes.
- **Background-color zoning** (IBM): Alternate between `#ffffff` and `var(--surface-elevated)` to create section separation with minimal vertical space.
- **Compression within, expansion between** (Apple): Text blocks are tight (negative tracking, compact line-heights); the space surrounding them is generous.

### Border Radius Scale

| Token | Value | Use |
|-------|-------|-----|
| `--radius-none` | 0px | Document elements, IBM-style enterprise contexts |
| `--radius-sm` | 4px | Small interactive elements, badges inner |
| `--radius-md` | 6px | Buttons, inputs, functional elements |
| `--radius-lg` | 8px | Cards, panels, containers |
| `--radius-xl` | 12px | Featured cards, image containers |
| `--radius-pill` | 24px | Status badges, tags (IBM exception) |
| `--radius-full` | 9999px | Navigation pills, large rounded elements |

## 6. Depth & Elevation

| Level | Treatment | Use |
|-------|-----------|-----|
| Flat (Level 0) | No shadow, `var(--surface-page)` | Default page surface |
| Surface (Level 1) | Background shift to `var(--surface-elevated)` | Cards, alternating sections (IBM approach) |
| Ambient (Level 2) | `var(--shadow-ambient) 0px 3px 6px` | Subtle card lift |
| Elevated (Level 3) | `var(--shadow-brand) 0px 20px 35px -20px, var(--shadow-neutral) 0px 12px 24px -12px` | Featured cards, dropdowns (Stripe approach) |
| Floating (Level 4) | `var(--shadow-brand) 0px 30px 45px -20px, var(--shadow-neutral) 0px 18px 36px -18px` | Modals, floating panels |
| Glass (Navigation) | `backdrop-filter: saturate(180%) blur(20px)` on translucent bg | Sticky navigation (Apple) |
| Focus | `2px solid var(--monacai-blue-deep)` outline | Keyboard focus ring |

### Shadow Philosophy

MonacAI uses navy-tinted shadows (`rgba(10,35,66,0.25)`) adapted from Stripe's blue-tinted approach. The navy tint connects elevation to the maritime brand palette -- shadows don't just add depth, they add brand atmosphere. Multi-layer shadows pair the branded tint (far, diffused) with a neutral black layer (close, tight) for parallax-like depth.

**Dark mode exception**: Following Linear's approach, dark mode uses luminance-based depth (progressively lighter backgrounds) rather than shadows. Shadows are invisible on dark surfaces.

## 7. Do's and Don'ts

### Do
- Use Inter with negative letter-spacing at display sizes (-1.4px at 56px, progressive relaxation)
- Use `var(--text-primary)` deep navy (`#0A2342`) for headings -- not pure black
- Apply `"tnum"` on ALL numeric data displays -- financial figures, metrics, table numbers
- Use navy-tinted shadows (`var(--shadow-brand)`) for elevated elements
- Use D-DIN uppercase with positive tracking for technical classification labels
- Use IBM Plex Mono for all metric/data/code displays
- Reference CSS custom properties (`var(--monacai-*)`) for all colors
- Use background-color zoning (white/gray alternation) for section separation
- Keep border-radius between 6-12px for interactive elements (conservative rounding)
- Use semantic status colors (red/amber/green/blue) consistently across all projects

### Don't
- Don't use pure black (`#000000`) for headings -- always deep navy
- Don't use shadows in dark mode -- use luminance stepping instead
- Don't mix Inter and IBM Plex Sans in the same heading hierarchy -- pick one per project variant
- Don't use weight 700+ on Inter body text -- 600 is the maximum
- Don't use the WOSA Red (`#A61B2B`) or VesselWise Teal (`#35464A`) for general interactive elements -- these are reserved for their respective brand contexts
- Don't add decorative gradients or textures -- solid colors only
- Don't skip tabular numerals on financial/metric data
- Don't use positive letter-spacing on Inter (except at 12px caption with 0.32px for readability)
- Don't introduce additional accent colors beyond the defined palette
- Don't use em dashes in WOSA documents -- hard rule from WOSA formatting standard

## 8. Responsive Behavior

### Breakpoints

| Name | Width | Key Changes |
|------|-------|-------------|
| Mobile | <640px | Single column, reduced heading sizes, stacked cards |
| Tablet | 640-1024px | 2-column grids, moderate padding |
| Desktop | 1024-1280px | Full layout, 3-column feature grids |
| Large Desktop | >1280px | Centered content with generous margins, max-width 1200px |

### Touch Targets
- Minimum interactive height: 44px
- Button padding: 10px 20px creating comfortable touch targets
- Navigation links: 56px row height
- Table rows: minimum 44px height for touch interaction

### Collapsing Strategy
- Hero: 56px display to 32px on mobile, weight 600 maintained
- Navigation: horizontal links to hamburger with full-screen overlay
- Dashboard grids: 3-column to 2-column to single column
- Metric cards: grid to vertical stack
- Data tables: horizontal scroll on mobile, sticky first column
- Section spacing: 64px+ to 32px on mobile

### Typography Scaling
- Display Hero: 56px to 36px on mobile
- Section Heading: 32px to 24px on mobile
- Body: 16px maintained at all sizes
- Metric Display: 48px to 32px on mobile

## 9. Agent Prompt Guide

### Quick Color Reference
- Primary accent: Maritime Blue (`#1c69d4`)
- Focus/active: Deep Blue (`#0653b6`)
- Background: White (`#ffffff`)
- Heading text: Deep Navy (`#0A2342`)
- Body text: Secondary (`#525252`)
- Border: Soft Blue (`#e5edf5`)
- Link: Maritime Blue (`#1c69d4`)
- Dark bg: Near-black (`#08090a`)
- Dark text: Near-white (`#f7f8f8`)
- Error/critical: Red (`#da1e28`)
- Success: Green (`#24a148`)
- Warning: Amber (`#f1c21b`)
- WOSA accent: Red (`#A61B2B`)
- WOSA sections: Teal (`#1A6B6E`)

### Example Component Prompts

- "Create a dashboard hero section on white background. Headline at 48px Inter weight 600, line-height 1.15, letter-spacing -0.96px, color #0A2342. Subtitle at 18px weight 400, line-height 1.56, color #525252. Primary button (#1c69d4 bg, white text, 6px radius, 10px 20px padding) and secondary button (transparent, 1px solid #e5edf5, #1c69d4 text, 6px radius)."

- "Design a KPI metric card: white background, shadow rgba(10,35,66,0.25) 0px 20px 35px -20px, rgba(0,0,0,0.1) 0px 12px 24px -12px. 8px radius. Metric value at 48px IBM Plex Mono weight 300, font-feature-settings 'tnum', color #0A2342. Label at 12px Inter weight 500, uppercase, letter-spacing 0.32px, color #757575. Delta indicator in #24a148 (up) or #da1e28 (down)."

- "Build a data table: header row #f4f4f4 background. Header text Inter 12px weight 600, uppercase, 0.32px tracking, #0A2342. Body text Inter 14px weight 400 for descriptions, IBM Plex Mono 14px 'tnum' for numbers. Alternating rows white/#f4f4f4. Border 0.5px solid #ebebeb."

- "Create a status badge: 24px pill radius, 4px 10px padding. Critical: rgba(218,30,40,0.15) bg, #da1e28 text. Compliant: rgba(36,161,72,0.15) bg, #24a148 text. Warning: rgba(241,194,27,0.15) bg, #946300 text."

- "Design a dark mode dashboard panel: #191a1b background, 8px radius, 1px solid rgba(255,255,255,0.08) border. Title at 20px Inter weight 600, color #f7f8f8. Metric at 32px IBM Plex Mono weight 300, 'tnum', color #2997ff. Caption at 12px Inter weight 400, color #8a8f98."

### Iteration Guide

1. Heading color is always `#0A2342` (deep navy) on light, `#f7f8f8` on dark -- never pure black
2. All numbers in tables/metrics/charts use IBM Plex Mono with `"tnum"` -- no exceptions
3. Shadow formula: `rgba(10,35,66,0.25) 0px Y1 B1 -S1, rgba(0,0,0,0.1) 0px Y2 B2 -S2` (navy-tinted far + neutral close)
4. D-DIN uppercase with 1.0px tracking for technical classification labels only
5. Three Inter weights: 400 (read), 500 (interact), 600 (announce)
6. Border-radius: 6px buttons, 8px cards, 24px badges -- nothing else
7. Status colors: red (#da1e28), amber (#f1c21b), green (#24a148), blue (#0f62fe) -- consistent everywhere
8. Dark mode depth via background luminance stepping: #08090a to #0f1011 to #191a1b to #28282c
9. WOSA documents: Inter family, WOSA Red (#A61B2B) headers, Teal (#1A6B6E) sections, no em dashes
10. Always define colors via CSS custom properties for cross-project consistency
