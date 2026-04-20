# Ferretti Group KPI Dashboard — Design System Variant
**WOSA Surveys · Executive Intelligence Platform**

A purpose-built design language for executive-facing KPI dashboards delivered to Ferretti Group. This variant extends the MonacAI master DESIGN.md with IBM Carbon authority, data-dense layouts optimized for 1920×1080 presentation screens, and the full semantic token stack required for performance, quality, and risk visualization.

> **Relationship to master DESIGN.md**: This file overrides or specializes Sections 2–8 for the FG KPI dashboard context. Where this document is silent, the master DESIGN.md governs. Never mix Inter and IBM Plex Sans in the same heading hierarchy within a single dashboard — this variant uses IBM Plex Sans exclusively.

---

## 1. Visual Theme & Atmosphere

The FG KPI dashboard communicates enterprise authority, operational clarity, and analytic rigor. The aesthetic draws directly from IBM Carbon's Gray 100 design language: cool neutral surfaces, zero decorative radius on interactive controls, background-color layering as the primary depth mechanism, and typographic precision as the primary visual tool.

**Design register:** Two-mode system.

- **Light Mode (Day)** — Gray 10 (`#f4f4f4`) canvas with White (`#ffffff`) cards. Used for print exports, shared PDFs, and on-site review.
- **Dark Mode (Presentation)** — Gray 100 (`#161616`) canvas with Gray 90 (`#262626`) and Gray 80 (`#393939`) layering. Used for boardroom presentation, large-screen display, and ambient monitoring.

**Key Characteristics:**

- IBM Plex Sans as the single typeface for all UI text — headers, labels, body, captions
- IBM Plex Mono exclusively for all numeric data, metrics, deltas, percentages, and table figures
- IBM Blue 60 (`#0f62fe`) as the sole interactive accent
- WOSA Red (`#A61B2B`) confined strictly to document headers and the WOSA logo lockup
- Zero border-radius on buttons and inputs — IBM Carbon signature
- 8px border-radius on cards and panels only
- Background-color layering for depth; shadows suppressed in favor of luminance stepping
- 8px spacing grid — strict adherence, no exceptions
- `"tnum"` tabular numerals on every rendered number, without exception
- Full CDS semantic status token stack for all status and risk visualization
- Data-dense layout targeting 1920×1080 (Full HD) as the design viewport
- 16-column grid for maximum information density at FHD resolution

---

## 2. Color Palette & Roles

### CSS Custom Properties

```css
:root {
  /* ── IBM Neutral Scale (light mode) ─────────────────────────────── */
  --cds-background:         #ffffff;   /* Primary page background */
  --cds-layer-01:           #f4f4f4;   /* Gray 10 — cards, alternating rows */
  --cds-layer-02:           #e8e8e8;   /* Gray 20 — nested panels, sub-cards */
  --cds-layer-03:           #d1d1d1;   /* Gray 30 — tertiary surfaces */
  --cds-border-subtle:      #c6c6c6;   /* Gray 40 — subtle dividers */
  --cds-border-strong:      #8d8d8d;   /* Gray 50 — visible borders, table rules */
  --cds-text-primary:       #161616;   /* Gray 100 — primary body text */
  --cds-text-secondary:     #525252;   /* Gray 70 — secondary labels */
  --cds-text-placeholder:   #6f6f6f;   /* Gray 60 — placeholder, disabled */
  --cds-text-disabled:      #a8a8a8;   /* Gray 45 — inactive elements */
  --cds-text-on-color:      #ffffff;   /* White on dark/colored backgrounds */
  --cds-icon-primary:       #161616;   /* Gray 100 — primary icons */
  --cds-icon-secondary:     #525252;   /* Gray 70 — secondary icons */

  /* ── IBM Neutral Scale (dark mode — Gray 100 theme) ─────────────── */
  --cds-background-dark:    #161616;   /* Gray 100 — darkest canvas */
  --cds-layer-01-dark:      #262626;   /* Gray 90 — cards, primary surfaces */
  --cds-layer-02-dark:      #393939;   /* Gray 80 — nested panels */
  --cds-layer-03-dark:      #525252;   /* Gray 70 — tertiary elevated elements */
  --cds-border-subtle-dark: #393939;   /* Gray 80 — subtle dividers on dark */
  --cds-border-strong-dark: #6f6f6f;   /* Gray 60 — visible borders on dark */
  --cds-text-primary-dark:  #f4f4f4;   /* Gray 10 — primary text on dark */
  --cds-text-secondary-dark:#c6c6c6;   /* Gray 40 — secondary text on dark */
  --cds-text-disabled-dark: #525252;   /* Gray 70 — disabled on dark */

  /* ── IBM Blue 60 — Primary Interactive Accent ────────────────────── */
  --cds-interactive:        #0f62fe;   /* Blue 60 — primary CTA, links, focus */
  --cds-interactive-hover:  #0353e9;   /* Blue 70 — hover state */
  --cds-interactive-active: #002d9c;   /* Blue 80 — active/pressed state */
  --cds-interactive-dark:   #4589ff;   /* Blue 50 — interactive on dark canvas */
  --cds-focus:              #0f62fe;   /* Blue 60 — focus ring */
  --cds-focus-dark:         #ffffff;   /* White — focus ring on dark */
  --cds-highlight:          rgba(15, 98, 254, 0.12); /* Subtle selection highlight */

  /* ── Semantic Status Tokens (CDS full stack) ─────────────────────── */
  --cds-support-error:      #da1e28;   /* Red 60 — critical, failed, danger */
  --cds-support-error-bg:   #fff1f1;   /* Red 10 — error background tint */
  --cds-support-error-dark: #ff8389;   /* Red 40 — error on Gray 100 theme */
  --cds-support-success:    #24a148;   /* Green 50 — compliant, on-target, positive */
  --cds-support-success-bg: #defbe6;   /* Green 10 — success background tint */
  --cds-support-success-dark:#42be65;  /* Green 40 — success on Gray 100 theme */
  --cds-support-warning:    #f1c21b;   /* Yellow 30 — at-risk, attention required */
  --cds-support-warning-bg: #fcf4d6;   /* Yellow 10 — warning background tint */
  --cds-support-warning-dark:#f1c21b;  /* Yellow 30 — warning on dark (unchanged) */
  --cds-support-info:       #0f62fe;   /* Blue 60 — informational */
  --cds-support-info-bg:    #edf5ff;   /* Blue 10 — info background tint */
  --cds-support-info-dark:  #4589ff;   /* Blue 50 — info on Gray 100 theme */

  /* ── WOSA Brand (header use only) ───────────────────────────────── */
  --wosa-red:               #A61B2B;   /* WOSA Red — document headers, logo rule, brand stripe only */
  --wosa-red-rule:          #A61B2B;   /* 2px horizontal rule beneath document header */

  /* ── KPI Dashboard Accent — Data Visualization Series ───────────── */
  --chart-1:                #0f62fe;   /* Blue 60 — primary series */
  --chart-2:                #6fdc8c;   /* Green 30 — secondary series */
  --chart-3:                #d2a106;   /* Yellow 40 — tertiary series */
  --chart-4:                #ff832b;   /* Orange 40 — quaternary series */
  --chart-5:                #be95ff;   /* Purple 40 — fifth series */
  --chart-6:                #08bdba;   /* Teal 40 — sixth series */
  --chart-neg:              #da1e28;   /* Red 60 — negative delta, below target */
  --chart-pos:              #24a148;   /* Green 50 — positive delta, above target */
  --chart-neutral:          #8d8d8d;   /* Gray 50 — flat, no-change state */
}
```

### Status Color Usage Matrix

| Status | Token | Hex | Hex (Dark) | Use in Dashboard |
|--------|-------|-----|------------|------------------|
| Critical | `--cds-support-error` | `#da1e28` | `#ff8389` | KPI below critical threshold, overdue action items, red risk cells |
| Warning | `--cds-support-warning` | `#f1c21b` | `#f1c21b` | KPI approaching threshold, medium-priority items, amber risk cells |
| On Target | `--cds-support-success` | `#24a148` | `#42be65` | KPI within target range, completed items, green cells |
| Informational | `--cds-support-info` | `#0f62fe` | `#4589ff` | Reference data, footnotes, contextual callouts |
| WOSA Brand | `--wosa-red` | `#A61B2B` | `#A61B2B` | Header rule and logo lockup only — never on data elements |

**Rule:** Status color on a background must achieve WCAG AA (4.5:1 for body text, 3:1 for large text or icons). Use the `-bg` tint variants for large colored areas; use the full saturated token for text on white or text on `--cds-layer-01`.

---

## 3. Typography Rules

### Font Families

| Role | Font | Source | Fallbacks |
|------|------|--------|-----------|
| All UI text — headings, labels, body, captions | IBM Plex Sans | Google Fonts (free) | Helvetica Neue, Arial, sans-serif |
| All numeric data — metrics, deltas, tables, charts | IBM Plex Mono | Google Fonts (free) | SFMono-Regular, Menlo, Consolas, monospace |

**Google Fonts import:**

```css
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@300;400;500;600;700&family=IBM+Plex+Mono:wght@300;400;500&display=swap');
```

### Type Scale & Hierarchy

| Role | Font | Size | Weight | Line Height | Letter Spacing | Features | Notes |
|------|------|------|--------|-------------|----------------|----------|-------|
| Dashboard Title | IBM Plex Sans | 28px | 600 | 1.25 | -0.3px | — | Report/page title |
| Section Heading | IBM Plex Sans | 20px | 600 | 1.30 | -0.2px | — | Widget headers, panel titles |
| Sub-heading | IBM Plex Sans | 16px | 600 | 1.375 | 0 | — | Card sub-titles |
| Body | IBM Plex Sans | 14px | 400 | 1.43 | 0.16px | — | Table text, descriptions |
| Label | IBM Plex Sans | 12px | 500 | 1.33 | 0.32px | uppercase | KPI card labels, column headers |
| Caption | IBM Plex Sans | 11px | 400 | 1.33 | 0.32px | — | Footnotes, timestamps, data sources |
| KPI Hero | IBM Plex Mono | 56px | 300 | 1.00 | 0 | tnum | Large primary KPI number |
| KPI Large | IBM Plex Mono | 40px | 300 | 1.00 | 0 | tnum | Secondary KPI numbers |
| KPI Medium | IBM Plex Mono | 28px | 400 | 1.07 | 0 | tnum | Tertiary metrics, gauge values |
| Delta Value | IBM Plex Mono | 14px | 500 | 1.29 | 0 | tnum | +/- change indicators |
| Table Number | IBM Plex Mono | 13px | 400 | 1.29 | 0.16px | tnum | All numeric table cells |
| Table Text | IBM Plex Sans | 13px | 400 | 1.29 | 0.16px | — | Non-numeric table cells |
| Chart Axis | IBM Plex Mono | 11px | 400 | 1.33 | 0 | tnum | Axis tick labels |
| Chart Label | IBM Plex Sans | 11px | 400 | 1.33 | 0.16px | — | Series labels, chart captions |

### OpenType Feature Requirements

```css
/* Apply to all numeric elements — non-negotiable */
.kpi-value,
.delta-value,
[data-metric],
td.numeric,
th.numeric {
  font-family: 'IBM Plex Mono', 'SFMono-Regular', Menlo, Consolas, monospace;
  font-feature-settings: 'tnum' 1, 'zero' 1;
  font-variant-numeric: tabular-nums lining-nums;
}

/* Apply to all text elements */
body,
.dashboard-label,
.section-heading {
  font-family: 'IBM Plex Sans', 'Helvetica Neue', Arial, sans-serif;
  font-feature-settings: 'liga' 1, 'kern' 1;
}
```

**Absolute rule:** If a character is a digit (0–9), a decimal point, a percentage sign, a currency symbol adjacent to a number, or a +/- delta indicator, it must render in IBM Plex Mono with `font-feature-settings: 'tnum' 1`. No exceptions. Mixing proportional and tabular numerals in a column invalidates the comparative read.

---

## 4. Component Library

### 4.1 WOSA Document Header

The standard header block appears at the top of every dashboard page and exported report. It is the only location where `--wosa-red` appears.

```
┌─────────────────────────────────────────────────────────────────────┐
│  [WOSA LOGO]                              Ferretti Group S.p.A.      │
│  WOSA Surveys                             Via Irma Bandiera 62       │
│  World Ocean Survey Auditing              47841 Cattolica (RN)       │
│                                           Italy                      │
├─────────────────────────────────────────────────────────────────────┤  ← 2px solid #A61B2B
```

**Spec:**
- Container: `height: 72px` (3× 8px base), `padding: 16px 32px`
- Background: `var(--cds-background)` (white in light), `var(--cds-layer-01-dark)` (dark)
- WOSA logo: Left-aligned, height 36px, `filter: none` (color logo)
- Company block: Right-aligned, IBM Plex Sans 12px weight 400, `var(--cds-text-secondary)` — address details
- Company name: IBM Plex Sans 14px weight 600, `var(--cds-text-primary)`
- Rule: `border-bottom: 2px solid var(--wosa-red)` — immediately below the header block

```css
.wosa-doc-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 72px;
  padding: 0 32px;
  background: var(--cds-background);
  border-bottom: 2px solid var(--wosa-red);
}

.wosa-doc-header__logo {
  height: 36px;
  width: auto;
}

.wosa-doc-header__company {
  text-align: right;
  font-family: 'IBM Plex Sans', sans-serif;
}

.wosa-doc-header__company-name {
  font-size: 14px;
  font-weight: 600;
  color: var(--cds-text-primary);
  line-height: 1.29;
}

.wosa-doc-header__company-detail {
  font-size: 11px;
  font-weight: 400;
  color: var(--cds-text-secondary);
  line-height: 1.45;
  letter-spacing: 0.16px;
}
```

---

### 4.2 KPI Metric Cards

The primary data-communication unit of the dashboard. Each card presents a single business metric with its current value, period delta, and optional sparkline.

**Layout anatomy (from top):**
1. Label row: metric name + optional status icon
2. Value row: primary KPI number (hero size)
3. Delta row: period-over-period change with directional indicator
4. Sparkline row: 8-week mini trend (optional, no axes)

**Card variants by size:**

| Variant | Grid span | KPI size | Use |
|---------|-----------|----------|-----|
| Hero | 4 cols | 56px | 1–2 primary KPIs per dashboard |
| Standard | 3 cols | 40px | Main metric grid (6–8 cards per row) |
| Compact | 2 cols | 28px | Secondary metrics, supporting data |

```css
/* Base card — shared by all variants */
.kpi-card {
  background: var(--cds-background);
  border: 1px solid var(--cds-border-subtle);
  border-radius: 8px;         /* 8px on cards only — see Section 7 */
  padding: 20px 24px;
  position: relative;
  overflow: hidden;
}

/* Status stripe — 4px left border indicating overall status */
.kpi-card[data-status="critical"] { border-left: 4px solid var(--cds-support-error); }
.kpi-card[data-status="warning"]  { border-left: 4px solid var(--cds-support-warning); }
.kpi-card[data-status="success"]  { border-left: 4px solid var(--cds-support-success); }
.kpi-card[data-status="info"]     { border-left: 4px solid var(--cds-support-info); }

.kpi-card__label {
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 11px;
  font-weight: 500;
  color: var(--cds-text-secondary);
  letter-spacing: 0.32px;
  text-transform: uppercase;
  margin-bottom: 8px;
}

.kpi-card__value {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 40px;          /* Override with 56px for Hero variant */
  font-weight: 300;
  line-height: 1.0;
  color: var(--cds-text-primary);
  font-feature-settings: 'tnum' 1, 'zero' 1;
  font-variant-numeric: tabular-nums lining-nums;
  letter-spacing: 0;
  margin-bottom: 8px;
}

.kpi-card__delta {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 13px;
  font-weight: 500;
  font-feature-settings: 'tnum' 1;
  letter-spacing: 0;
}

/* Delta directional color */
.kpi-card__delta--up    { color: var(--cds-support-success); }
.kpi-card__delta--down  { color: var(--cds-support-error); }
.kpi-card__delta--flat  { color: var(--cds-text-placeholder); }

.kpi-card__delta-period {
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 11px;
  font-weight: 400;
  color: var(--cds-text-placeholder);
  margin-left: 4px;
}

/* Sparkline container — no axes, no labels */
.kpi-card__sparkline {
  margin-top: 12px;
  height: 32px;
  width: 100%;
}

/* Dark mode overrides */
[data-theme="dark"] .kpi-card {
  background: var(--cds-layer-01-dark);
  border-color: var(--cds-border-subtle-dark);
}

[data-theme="dark"] .kpi-card__value {
  color: var(--cds-text-primary-dark);
}

[data-theme="dark"] .kpi-card__delta--up   { color: var(--cds-support-success-dark); }
[data-theme="dark"] .kpi-card__delta--down { color: var(--cds-support-error-dark); }
```

---

### 4.3 Performance Trend Charts

Chart containers for time-series data. The container is spec'd; the chart library renders within it.

**Supported chart types for this component:**
- Line chart — continuous trend (preferred for all time-series KPIs)
- Area chart — cumulative progress toward a target band
- Bar chart — period-discrete values (monthly, quarterly)

```css
.trend-chart-container {
  background: var(--cds-background);
  border: 1px solid var(--cds-border-subtle);
  border-radius: 8px;
  padding: 20px 24px 16px;
}

.trend-chart-container__header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  margin-bottom: 16px;
}

.trend-chart-container__title {
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 14px;
  font-weight: 600;
  color: var(--cds-text-primary);
  line-height: 1.375;
}

.trend-chart-container__subtitle {
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 11px;
  font-weight: 400;
  color: var(--cds-text-secondary);
  margin-top: 2px;
  letter-spacing: 0.16px;
}

/* Chart area — chart library fills this */
.trend-chart-container__canvas {
  width: 100%;
  height: 240px;       /* Default; 160px compact, 320px expanded */
  display: block;
}

/* Axis label style (apply via chart library config, not CSS) */
/* font: 'IBM Plex Mono' 11px, color: var(--cds-text-secondary) */
/* Grid lines: var(--cds-border-subtle), 0.5px, dashed */
/* Target line: var(--cds-interactive) Blue 60, 1.5px dashed */
/* Threshold line: var(--cds-support-error) Red 60, 1px solid */
```

**Chart configuration rules:**
- Axis ticks: IBM Plex Mono 11px, `var(--cds-text-secondary)`, `font-feature-settings: 'tnum' 1`
- Grid lines: `var(--cds-border-subtle)`, 0.5px, horizontal only (no vertical grid)
- Target reference line: `var(--cds-interactive)`, 1.5px dashed
- Critical threshold line: `var(--cds-support-error)`, 1px solid
- Tooltips: `var(--cds-layer-02)` background, 8px radius, IBM Plex Mono values
- No legend unless 3+ series; direct labels preferred

---

### 4.4 Action Item Tables

Priority-ranked tables for remediation actions, follow-up tasks, and owner assignments.

```css
.action-table {
  width: 100%;
  border-collapse: collapse;
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 13px;
}

.action-table th {
  background: var(--cds-layer-01);
  color: var(--cds-text-primary);
  font-size: 11px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.32px;
  padding: 10px 16px;
  text-align: left;
  border-bottom: 2px solid var(--cds-border-strong);
  white-space: nowrap;
}

.action-table td {
  padding: 10px 16px;
  border-bottom: 1px solid var(--cds-border-subtle);
  color: var(--cds-text-primary);
  vertical-align: top;
  line-height: 1.43;
}

/* Alternating rows */
.action-table tbody tr:nth-child(even) td {
  background: var(--cds-layer-01);
}

/* Numeric cells */
.action-table td.numeric,
.action-table th.numeric {
  font-family: 'IBM Plex Mono', monospace;
  font-feature-settings: 'tnum' 1;
  text-align: right;
}

/* Priority badge — inline in table cell */
.priority-badge {
  display: inline-flex;
  align-items: center;
  padding: 2px 8px;
  border-radius: 0;       /* IBM Carbon — 0px radius on table badges */
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.32px;
  text-transform: uppercase;
  white-space: nowrap;
}

.priority-badge--p1 {
  background: var(--cds-support-error-bg);
  color: var(--cds-support-error);
  border-left: 2px solid var(--cds-support-error);
}

.priority-badge--p2 {
  background: var(--cds-support-warning-bg);
  color: #6a4000;          /* Dark amber — sufficient contrast on yellow tint */
  border-left: 2px solid var(--cds-support-warning);
}

.priority-badge--p3 {
  background: var(--cds-support-info-bg);
  color: var(--cds-support-info);
  border-left: 2px solid var(--cds-support-info);
}

.priority-badge--closed {
  background: var(--cds-support-success-bg);
  color: var(--cds-support-success);
  border-left: 2px solid var(--cds-support-success);
}
```

**Recommended columns:** Priority | Action Description | Area / System | Owner | Due Date | Status | Days Overdue

---

### 4.5 Risk Heatmaps

Probability × Impact matrix for risk visualization. Rendered as a fixed 5×5 CSS grid.

```css
.risk-heatmap {
  display: grid;
  grid-template-columns: 40px repeat(5, 1fr);
  grid-template-rows: repeat(5, 1fr) 24px;
  gap: 2px;
  font-family: 'IBM Plex Sans', sans-serif;
}

/* Cell base */
.risk-heatmap__cell {
  aspect-ratio: 1.2;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 13px;
  font-weight: 500;
  font-feature-settings: 'tnum' 1;
  border-radius: 0;     /* No radius on heatmap cells */
  position: relative;
}

/* Risk level fill colors */
.risk-heatmap__cell--critical  { background: #750e13; color: #ffffff; }   /* Red 80 */
.risk-heatmap__cell--high      { background: #da1e28; color: #ffffff; }   /* Red 60 */
.risk-heatmap__cell--medium    { background: #f1c21b; color: #161616; }   /* Yellow 30 */
.risk-heatmap__cell--low       { background: #24a148; color: #ffffff; }   /* Green 50 */
.risk-heatmap__cell--minimal   { background: #defbe6; color: #0e6027; }   /* Green 10 + Green 70 */

/* Cell containing a risk item — adds a dot indicator */
.risk-heatmap__cell--occupied::after {
  content: attr(data-count);
  position: absolute;
  top: 4px;
  right: 6px;
  font-size: 10px;
  font-weight: 600;
  opacity: 0.9;
}

/* Axis labels */
.risk-heatmap__y-label {
  writing-mode: vertical-rl;
  transform: rotate(180deg);
  font-size: 10px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.32px;
  color: var(--cds-text-secondary);
  text-align: center;
}

.risk-heatmap__x-label {
  font-size: 10px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.32px;
  color: var(--cds-text-secondary);
  text-align: center;
  padding-top: 4px;
}
```

**Standard risk matrix thresholds:**

| Score | Color Token | Severity |
|-------|-------------|----------|
| 20–25 | `#750e13` Red 80 | Critical — immediate escalation |
| 12–19 | `#da1e28` Red 60 | High — corrective action within 30 days |
| 6–11 | `#f1c21b` Yellow 30 | Medium — scheduled action plan |
| 2–5 | `#24a148` Green 50 | Low — monitor only |
| 1 | `#defbe6` Green 10 | Minimal — accept and log |

---

### 4.6 Quality Score Gauges

Semi-circular gauge for composite quality scores, certification compliance percentages, and audit ratings.

```
        ╭──────────────────╮
       ╱  Score Arc         ╲
      │   ┌────────────┐     │
      │   │   97.3     │     │
      │   │   ─────    │     │
      │   │  QUALITY   │     │
       ╲  └────────────┘    ╱
        ╰──────────────────╯
         Min              Max
         0               100
```

**Gauge spec:**
- Arc width: 12px (responsive: 8px compact)
- Track color: `var(--cds-layer-02)` (empty arc background)
- Score arc: interpolated from `--cds-support-error` (0–59) → `--cds-support-warning` (60–79) → `--cds-support-success` (80–100)
- Center value: IBM Plex Mono, 28px weight 400, `"tnum"`, `var(--cds-text-primary)`
- Center label: IBM Plex Sans, 10px weight 500, uppercase, `var(--cds-text-secondary)`
- Target marker: 2px tick mark at target position, `var(--cds-interactive)` Blue 60
- Preferred implementation: SVG `<path>` with `stroke-dasharray` animation

```css
.quality-gauge {
  position: relative;
  width: 160px;     /* Compact: 120px, Expanded: 200px */
  aspect-ratio: 1;
}

.quality-gauge__value {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 28px;
  font-weight: 400;
  font-feature-settings: 'tnum' 1;
  color: var(--cds-text-primary);
  text-anchor: middle;
  dominant-baseline: middle;
}

.quality-gauge__label {
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 10px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.32px;
  fill: var(--cds-text-secondary);
  text-anchor: middle;
}
```

---

### 4.7 Monthly Comparison Tables

Side-by-side multi-period comparison tables for tracking KPIs across months, quarters, or vessels.

```css
.comparison-table {
  width: 100%;
  border-collapse: collapse;
}

/* Fixed first column — metric name */
.comparison-table td:first-child,
.comparison-table th:first-child {
  position: sticky;
  left: 0;
  background: inherit;
  z-index: 1;
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 13px;
  font-weight: 500;
  min-width: 180px;
  border-right: 2px solid var(--cds-border-strong);
}

/* Period column headers */
.comparison-table th {
  background: var(--cds-layer-01);
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 11px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.32px;
  color: var(--cds-text-primary);
  padding: 10px 12px;
  text-align: right;
  border-bottom: 2px solid var(--cds-border-strong);
  white-space: nowrap;
  min-width: 88px;
}

/* Data cells — all numeric */
.comparison-table td.data-cell {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 13px;
  font-weight: 400;
  font-feature-settings: 'tnum' 1;
  text-align: right;
  padding: 9px 12px;
  border-bottom: 1px solid var(--cds-border-subtle);
  color: var(--cds-text-primary);
  white-space: nowrap;
}

/* Current-period column highlight */
.comparison-table th.current-period,
.comparison-table td.current-period {
  background: rgba(15, 98, 254, 0.06);
  font-weight: 500;
}

/* In-cell delta pill — rendered within numeric cell */
.inline-delta {
  display: inline-flex;
  align-items: center;
  gap: 2px;
  font-size: 11px;
  font-family: 'IBM Plex Mono', monospace;
  font-feature-settings: 'tnum' 1;
  margin-left: 6px;
  padding: 1px 4px;
}

.inline-delta--up   { color: var(--cds-support-success); }
.inline-delta--down { color: var(--cds-support-error); }
.inline-delta--flat { color: var(--cds-text-placeholder); }

/* Row group separators (vessel sections, category breaks) */
.comparison-table tr.group-header td {
  background: var(--cds-layer-02);
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 11px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.32px;
  color: var(--cds-text-secondary);
  padding: 6px 12px;
  border-top: 1px solid var(--cds-border-strong);
}
```

---

### 4.8 Buttons & Inputs

**IBM Carbon signature: 0px border-radius on all interactive controls.**

```css
/* Primary Button */
.btn-primary {
  display: inline-flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  height: 48px;
  padding: 0 16px;
  background: var(--cds-interactive);
  color: #ffffff;
  border: none;
  border-radius: 0;                    /* IBM Carbon — 0px */
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 14px;
  font-weight: 400;
  letter-spacing: 0.16px;
  cursor: pointer;
  transition: background 70ms linear;
}

.btn-primary:hover  { background: var(--cds-interactive-hover); }
.btn-primary:active { background: var(--cds-interactive-active); }
.btn-primary:focus-visible {
  outline: 2px solid var(--cds-focus);
  outline-offset: 2px;
}

/* Secondary Button */
.btn-secondary {
  height: 48px;
  padding: 0 16px;
  background: var(--cds-layer-01);
  color: var(--cds-interactive);
  border: 1px solid var(--cds-interactive);
  border-radius: 0;
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 14px;
  font-weight: 400;
  letter-spacing: 0.16px;
  cursor: pointer;
}

.btn-secondary:hover  { background: var(--cds-layer-02); }

/* Ghost Button */
.btn-ghost {
  height: 48px;
  padding: 0 16px;
  background: transparent;
  color: var(--cds-interactive);
  border: none;
  border-radius: 0;
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 14px;
  font-weight: 400;
  letter-spacing: 0.16px;
  cursor: pointer;
}

.btn-ghost:hover { background: var(--cds-highlight); }

/* Danger Button */
.btn-danger {
  background: var(--cds-support-error);
  color: #ffffff;
  border: none;
  border-radius: 0;
  height: 48px;
  padding: 0 16px;
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 14px;
  font-weight: 400;
  letter-spacing: 0.16px;
  cursor: pointer;
}

/* Text Input & Select */
.cds-input {
  height: 40px;
  padding: 0 16px;
  background: var(--cds-layer-01);
  border: none;
  border-bottom: 1px solid var(--cds-border-strong);
  border-radius: 0;                    /* IBM Carbon — 0px */
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 14px;
  color: var(--cds-text-primary);
  width: 100%;
  outline: none;
  transition: border-color 70ms linear;
}

.cds-input:focus {
  border-bottom: 2px solid var(--cds-interactive);
}

.cds-input::placeholder {
  color: var(--cds-text-placeholder);
}
```

---

## 5. Layout Principles

### Spacing System (8px base — IBM Carbon)

| Token | Value | Use |
|-------|-------|-----|
| `--space-01` | 2px | Icon gap, micro nudge |
| `--space-02` | 4px | Tight badge padding |
| `--space-03` | 8px | Base unit — smallest component gap |
| `--space-04` | 12px | Compact internal padding |
| `--space-05` | 16px | Standard padding, label gap |
| `--space-06` | 24px | Card internal padding |
| `--space-07` | 32px | Section gap, card-to-card |
| `--space-08` | 40px | Panel section headers |
| `--space-09` | 48px | Major layout section breaks |
| `--space-10` | 64px | Maximum section spacing |

No spacing value that is not a multiple of 8 is permitted in layout geometry. The 4px (`--space-02`) exception applies only to inline elements (badge padding, icon gaps) — never to layout margins or component gaps.

### Grid — 1920×1080 (Primary Design Viewport)

```css
.dashboard-grid {
  display: grid;
  grid-template-columns: repeat(16, 1fr);
  column-gap: 16px;           /* Tight gutters for data density */
  row-gap: 16px;
  padding: 0 24px;
  max-width: 1920px;
  margin: 0 auto;
}

/* KPI card row — 8 cards across at 2 cols each */
.kpi-row    { grid-column: span 2; }
.kpi-wide   { grid-column: span 4; }
.kpi-hero   { grid-column: span 4; }

/* Chart panels */
.chart-half { grid-column: span 8; }
.chart-full { grid-column: span 16; }
.chart-third{ grid-column: span 5; }  /* ~3-across with remainder */

/* Table panels */
.table-full { grid-column: span 16; }
.table-half { grid-column: span 8; }

/* Sidebar panels */
.panel-narrow { grid-column: span 4; }
.panel-wide   { grid-column: span 12; }
```

**Standard dashboard page anatomy (top to bottom):**

1. WOSA Document Header (full width, 72px, outside grid)
2. Dashboard Title Bar (full width, 48px — report name, date range, filter controls)
3. KPI Hero Row (8× standard cards, or 2× hero + 4× standard)
4. Primary Content Row (chart 8-col + table/gauge 8-col)
5. Secondary Content Row (heatmap 8-col + comparison table 8-col)
6. Action Items Table (full 16-col)
7. Footer / Data Source Bar (full width, 32px, outside grid)

### Depth & Background-Color Layering

No box-shadow in the light mode default. Depth is created exclusively through background luminance stepping — IBM approach.

| Level | Light Mode bg | Dark Mode bg | Use |
|-------|--------------|--------------|-----|
| Page canvas | `#ffffff` | `#161616` Gray 100 | Document root |
| Layer 01 | `#f4f4f4` Gray 10 | `#262626` Gray 90 | Cards, panels, table headers |
| Layer 02 | `#e8e8e8` Gray 20 | `#393939` Gray 80 | Nested sub-panels, active rows |
| Layer 03 | `#d1d1d1` Gray 30 | `#525252` Gray 70 | Tertiary elevated surfaces |
| Interactive | Blue 60 tint | Blue 60 tint | Focused or selected rows |

**Exception:** A single ambient shadow is permitted for floating overlays (tooltips, dropdowns, modals) in light mode only: `box-shadow: 0 4px 8px rgba(0,0,0,0.12), 0 1px 3px rgba(0,0,0,0.08)`. Never on static card elements.

---

## 6. Dark Theme (Gray 100 — Presentation Mode)

Activated via `[data-theme="dark"]` on `<html>` or `<body>`. Used for boardroom presentations, large-screen displays, and after-hours monitoring contexts.

```css
[data-theme="dark"] {
  /* Canvas and layers */
  --cds-background:      var(--cds-background-dark);   /* #161616 */
  --cds-layer-01:        var(--cds-layer-01-dark);     /* #262626 */
  --cds-layer-02:        var(--cds-layer-02-dark);     /* #393939 */
  --cds-layer-03:        var(--cds-layer-03-dark);     /* #525252 */

  /* Borders */
  --cds-border-subtle:   var(--cds-border-subtle-dark);  /* #393939 */
  --cds-border-strong:   var(--cds-border-strong-dark);  /* #6f6f6f */

  /* Text */
  --cds-text-primary:    var(--cds-text-primary-dark);   /* #f4f4f4 */
  --cds-text-secondary:  var(--cds-text-secondary-dark); /* #c6c6c6 */
  --cds-text-placeholder:var(--cds-text-disabled-dark);  /* #525252 */

  /* Interactive */
  --cds-interactive:     var(--cds-interactive-dark);    /* #4589ff Blue 50 */
  --cds-highlight:       rgba(69, 137, 255, 0.16);

  /* Semantic — adjusted for dark canvas */
  --cds-support-error:   var(--cds-support-error-dark);   /* #ff8389 */
  --cds-support-success: var(--cds-support-success-dark); /* #42be65 */
  --cds-support-warning: var(--cds-support-warning-dark); /* #f1c21b */
  --cds-support-info:    var(--cds-support-info-dark);    /* #4589ff */

  /* Dark bg tints for status cells */
  --cds-support-error-bg:   rgba(255, 131, 137, 0.16);
  --cds-support-success-bg: rgba(66, 190, 101, 0.16);
  --cds-support-warning-bg: rgba(241, 194, 27, 0.16);
  --cds-support-info-bg:    rgba(69, 137, 255, 0.16);
}

/* WOSA header on dark — logo tinted to white, rule remains WOSA Red */
[data-theme="dark"] .wosa-doc-header {
  background: var(--cds-layer-01-dark);
  border-bottom-color: var(--wosa-red);  /* Red unchanged */
}

[data-theme="dark"] .wosa-doc-header__logo {
  filter: brightness(0) invert(1);  /* White logo on dark background */
}
```

---

## 7. Do's and Don'ts

### Do
- Use IBM Plex Sans for all text elements — no Inter in this variant
- Use IBM Plex Mono with `font-feature-settings: 'tnum' 1` for every number that appears in the dashboard
- Use `var(--cds-*)` custom property names for all color references — enables dark mode toggle via a single attribute change
- Apply `border-radius: 0` to all buttons, inputs, selects, and table badges
- Apply `border-radius: 8px` to cards, panels, chart containers, and gauges only
- Use background-color layering (Gray 10 → Gray 20 → Gray 30) for depth — no box-shadows on static elements
- Confine `--wosa-red` (`#A61B2B`) exclusively to the WOSA document header and logo rule
- Use Blue 60 (`#0f62fe`) as the sole interactive accent — links, focus rings, primary buttons
- Size your design at 1920×1080 first; confirm the 16-column grid fills cleanly
- Keep chart data-ink ratio high: horizontal grid lines only, no chart backgrounds, direct labels preferred over legends
- Use the 4px left border stripe on KPI cards to signal status (not fill background)
- Apply `text-transform: uppercase` and `letter-spacing: 0.32px` to all column headers and metric labels

### Don't
- Don't use Inter anywhere in this variant — IBM Plex Sans is the exclusive text typeface
- Don't use `--wosa-red` on data elements, status indicators, or KPI values — it is brand-only
- Don't introduce additional accent colors beyond the defined chart series palette
- Don't use positive letter-spacing on body text (14px+) or KPI values
- Don't apply box-shadows to cards or panels in the standard layout — use background layers instead
- Don't use border-radius on buttons, inputs, or table badges — `border-radius: 0` is mandatory
- Don't set any number in the layout using a proportional font — IBM Plex Mono + `"tnum"` is non-negotiable
- Don't use color as the only differentiator in tables or charts — always pair color with a text label, icon, or pattern
- Don't use mixed weight hierarchies on IBM Plex Mono — weight 300 for hero KPI, 400 for standard data, 500 for deltas and emphasis only
- Don't render pie charts for any data in this system — use bar charts for part-of-whole, stacked or otherwise
- Don't use em dashes in any WOSA document text — hard rule from WOSA formatting standard
- Don't abbreviate metric names in KPI card labels without a tooltip providing the full name

---

## 8. Responsive Behavior

This dashboard is designed for 1920×1080 as the primary viewport. The following breakpoints provide graceful degradation to smaller screens (shared PDFs, client portal web view).

| Name | Width | Grid | Card Columns | Notes |
|------|-------|------|-------------|-------|
| FHD (primary) | 1920px | 16-col, 16px gutter | 8× 2-col | Full design intent |
| HD | 1280px | 12-col, 16px gutter | 6× 2-col | Collapse narrow panels |
| Tablet | 1024px | 8-col, 16px gutter | 4× 2-col | Stack secondary content rows |
| Print / PDF | 1200px equiv | 12-col | 4-col cards | Export-safe layout, light mode forced |

```css
/* Breakpoints */
@media (max-width: 1280px) {
  .dashboard-grid { grid-template-columns: repeat(12, 1fr); }
  .chart-half     { grid-column: span 12; }   /* Stack charts full-width */
  .panel-narrow   { grid-column: span 12; }
  .panel-wide     { grid-column: span 12; }
}

@media (max-width: 1024px) {
  .dashboard-grid { grid-template-columns: repeat(8, 1fr); }
  .kpi-row        { grid-column: span 4; }
  .kpi-hero       { grid-column: span 8; }
  .chart-full,
  .table-full     { grid-column: span 8; }
}

/* Force light mode for print */
@media print {
  [data-theme="dark"] { --cds-background: #ffffff; }
  .wosa-doc-header__logo { filter: none; }
}
```

**Typography scaling:**

| Role | FHD (1920px) | HD (1280px) | Tablet (1024px) |
|------|-------------|------------|----------------|
| Dashboard Title | 28px | 24px | 20px |
| KPI Hero | 56px | 48px | 36px |
| KPI Large | 40px | 32px | 28px |
| KPI Medium | 28px | 24px | 20px |
| Body / Table | 13-14px | 13-14px | 13px |

---

## 9. Agent Prompt Guide

### Quick Token Reference

```
Canvas (light):          #ffffff
Layer 01 (cards):        #f4f4f4    Gray 10
Layer 02 (nested):       #e8e8e8    Gray 20
Border subtle:           #c6c6c6    Gray 40
Border strong:           #8d8d8d    Gray 50
Text primary:            #161616    Gray 100
Text secondary:          #525252    Gray 70
Text placeholder:        #6f6f6f    Gray 60
Interactive accent:      #0f62fe    Blue 60
Interactive hover:       #0353e9    Blue 70
Status error:            #da1e28    Red 60
Status warning:          #f1c21b    Yellow 30
Status success:          #24a148    Green 50
Status info:             #0f62fe    Blue 60
WOSA Red (header only):  #A61B2B

Canvas (dark):           #161616    Gray 100
Layer 01 dark:           #262626    Gray 90
Layer 02 dark:           #393939    Gray 80
Text primary dark:       #f4f4f4    Gray 10
Interactive dark:        #4589ff    Blue 50
Error dark:              #ff8389    Red 40
Success dark:            #42be65    Green 40
```

### Component Build Prompts

**KPI Metric Card (standard):**
> "Build a KPI metric card using IBM Carbon layer system. Background `#f4f4f4` (Gray 10), `border-radius: 8px`, `border: 1px solid #c6c6c6`, `padding: 20px 24px`. No box-shadow. Left-border status stripe: 4px solid (red `#da1e28` / amber `#f1c21b` / green `#24a148` based on status). Label: IBM Plex Sans 11px weight 500, uppercase, `letter-spacing: 0.32px`, color `#525252`. KPI value: IBM Plex Mono 40px weight 300, `font-feature-settings: 'tnum' 1`, color `#161616`. Delta row: IBM Plex Mono 13px weight 500 `'tnum'`, green `#24a148` for positive delta, red `#da1e28` for negative. Period label in IBM Plex Sans 11px `#6f6f6f`."

**Performance Trend Chart container:**
> "Create a chart panel: background `#ffffff`, `border: 1px solid #c6c6c6`, `border-radius: 8px`, `padding: 20px 24px`. Title in IBM Plex Sans 14px weight 600, `#161616`. Subtitle in IBM Plex Sans 11px `#525252`. Chart canvas `height: 240px` — render a line chart with axis ticks in IBM Plex Mono 11px `#525252` `'tnum'`. Horizontal grid lines only at `#e8e8e8` 0.5px. Target reference line at Blue 60 `#0f62fe` 1.5px dashed. No vertical grid. Direct series labels, no legend unless 3+ series."

**Action Item Table:**
> "Build a data table with IBM Carbon styling. Header row background `#f4f4f4`, text IBM Plex Sans 11px weight 600 uppercase `letter-spacing: 0.32px` color `#161616`, `border-bottom: 2px solid #8d8d8d`. Body rows: IBM Plex Sans 13px, alternating `#ffffff` / `#f4f4f4`. Numeric cells: IBM Plex Mono 13px `'tnum'` right-aligned. Priority badge: `border-radius: 0`, P1 = `#fff1f1` bg `#da1e28` text `2px left border`, P2 = `#fcf4d6` bg `#6a4000` text `2px amber left border`. No box-shadows. `border-collapse: collapse`."

**Risk Heatmap (5×5):**
> "Create a 5×5 CSS Grid risk matrix. Cells: `aspect-ratio: 1.2`, `border-radius: 0`, `border: 2px solid #ffffff` (separation). Fill colors: score 20-25 = `#750e13` white text; 12-19 = `#da1e28` white text; 6-11 = `#f1c21b` `#161616` text; 2-5 = `#24a148` white text; 1 = `#defbe6` `#0e6027` text. Cell count badge: IBM Plex Mono 10px absolute top-right. Axis labels: IBM Plex Sans 10px uppercase `letter-spacing: 0.32px` `#525252`."

**Quality Score Gauge (SVG):**
> "Render an SVG semi-circular gauge, 160px wide. Arc track: `stroke: #e8e8e8` 12px. Score arc: `stroke` interpolates from `#da1e28` (0-59) to `#f1c21b` (60-79) to `#24a148` (80-100). Target tick: 2px line at target position, `stroke: #0f62fe`. Center text: IBM Plex Mono 28px weight 400 `'tnum'` `#161616`. Sub-label: IBM Plex Sans 10px uppercase `letter-spacing: 0.32px` `#525252`. Animate arc via `stroke-dasharray` / `stroke-dashoffset` over 600ms ease-out."

**Monthly Comparison Table:**
> "Build a monthly comparison table: sticky first column (`min-width: 180px`, `border-right: 2px solid #8d8d8d`). Period column headers: IBM Plex Sans 11px weight 600 uppercase `#161616` `#f4f4f4` background right-aligned. Current period column: `background: rgba(15,98,254,0.06)` on both header and data cells. Data cells: IBM Plex Mono 13px weight 400 `'tnum'` right-aligned. In-cell delta pill: IBM Plex Mono 11px `'tnum'`, green `#24a148` up / red `#da1e28` down. Group header rows: `#e8e8e8` bg IBM Plex Sans 11px uppercase. Horizontal scroll on overflow, sticky first column maintained."

**WOSA Document Header:**
> "Create the WOSA document header bar: `height: 72px`, `padding: 0 32px`, `background: #ffffff`, `border-bottom: 2px solid #A61B2B`. Flexbox with `justify-content: space-between`, `align-items: center`. Left: WOSA logo `height: 36px`. Right: company name in IBM Plex Sans 14px weight 600 `#161616`, address lines in IBM Plex Sans 11px `#525252`, right-aligned. This red rule is the only use of `#A61B2B` on the page."

**Dark Mode Dashboard Panel:**
> "Apply `[data-theme='dark']` styling: root `background: #161616`. Cards: `background: #262626`, `border: 1px solid #393939`, `border-radius: 8px`. KPI value: IBM Plex Mono 40px weight 300 `'tnum'`, color `#f4f4f4`. Delta up: `#42be65`; delta down: `#ff8389`. Interactive accent: `#4589ff`. All depth via background stepping (#161616 → #262626 → #393939) -- no box-shadows. WOSA header: `background: #262626`, red rule `#A61B2B` unchanged, logo `filter: brightness(0) invert(1)`."

### Iteration Rules

1. IBM Plex Sans is the only text typeface — do not introduce Inter, Roboto, or any other font
2. Every digit rendered in the dashboard must use IBM Plex Mono with `font-feature-settings: 'tnum' 1` — no exceptions
3. All buttons and inputs: `border-radius: 0`. All cards and panels: `border-radius: 8px`. Nothing else.
4. `--wosa-red` (`#A61B2B`) appears only in the WOSA document header — never on data, status, or interactive elements
5. Depth is background-luminance only on static elements; `box-shadow` only on floating overlays
6. Blue 60 (`#0f62fe`) is the sole interactive accent — links, focus rings, primary CTA, info status
7. Status colors: error `#da1e28`, warning `#f1c21b`, success `#24a148`, info `#0f62fe` — consistent everywhere
8. Dark mode toggle: single `[data-theme="dark"]` attribute on `<html>` — all colors resolve via CSS custom properties
9. No pie charts — ever. Use horizontal bar for part-of-whole, stacked bar for distribution
10. All spacing must be a multiple of 8px; only badge/icon internal padding may use 4px
