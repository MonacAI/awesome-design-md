# MonacAI Design System -- Install Guide

How to drop each DESIGN.md file into the right project so Claude Code (and any AI agent) picks it up automatically.

---

## What You Have

| File | Lines | Purpose | Target Project |
|---|---|---|---|
| `DESIGN.md` | 407 | Master MonacAI system -- all shared tokens, typography, shadows, spacing | Every MonacAI repo (root-level) |
| `vesselwise-DESIGN.md` | 669 | VesselWise standards library + survey dashboard | VesselWise platform repo |
| `fg-kpi-DESIGN.md` | 1,114 | FG KPI executive dashboard (IBM Carbon) | FG dashboard repo / project |
| `wosa-docs-DESIGN.md` | 841 | WOSA PDF documents via ReportLab | WOSA document generation repo |

---

## Install Steps

### 1. Master DESIGN.md (every repo)

```bash
# Copy to the root of each MonacAI project
cp DESIGN.md /path/to/your-project/DESIGN.md
```

This file is the single source of truth. The three variants inherit from it and override only what they need. Every repo should have a copy so Claude Code always has access to the base tokens.

### 2. VesselWise Variant

```bash
# Rename to DESIGN.md in the VesselWise project root
cp vesselwise-DESIGN.md /path/to/vesselwise/DESIGN.md
```

Also keep a copy of the master as `DESIGN-base.md` in the same repo so the inheritance chain is clear:

```bash
cp DESIGN.md /path/to/vesselwise/DESIGN-base.md
```

### 3. FG KPI Dashboard Variant

```bash
cp fg-kpi-DESIGN.md /path/to/fg-kpi-dashboard/DESIGN.md
cp DESIGN.md /path/to/fg-kpi-dashboard/DESIGN-base.md
```

### 4. WOSA Documents Variant

```bash
cp wosa-docs-DESIGN.md /path/to/wosa-documents/DESIGN.md
cp DESIGN.md /path/to/wosa-documents/DESIGN-base.md
```

---

## How Claude Code Uses It

When Claude Code opens a project, it reads `DESIGN.md` at the repo root automatically. Any prompt asking it to build UI, style components, pick colors, or set typography will follow the tokens and rules in the file.

**What this means in practice:**
- "Build a metric card" -- Claude Code will use the exact shadow formula, border-radius, font stack, and color tokens from the DESIGN.md
- "Add a status badge" -- it will use the correct semantic colors (red/amber/green) with the right opacity backgrounds
- "Create a dark mode panel" -- it will apply the luminance stepping pattern (no shadows on dark mode)
- "Format a WOSA cover page" -- it will follow the exact ReportLab specs with WOSA Red top bar, teal title, Inter fonts

**The Section 9 Agent Prompt Guide** in each file gives Claude Code (and any LLM) copy-paste component recipes with exact pixel specs. This is the highest-leverage section -- it turns vague requests into pixel-perfect output.

---

## Font Setup

Each variant specifies its fonts. Make sure they are available in the project:

| Variant | Primary | Technical | Monospace |
|---|---|---|---|
| Master / VesselWise / WOSA | Inter | D-DIN | IBM Plex Mono |
| FG KPI Dashboard | IBM Plex Sans | -- | IBM Plex Mono |

**Inter** -- free from Google Fonts or rsms.me/inter
**D-DIN** -- free from dafontfree.io (DIN-heritage, used by SpaceX)
**IBM Plex Sans / Mono** -- free from Google Fonts or github.com/IBM/plex
**DM Sans** -- fallback display font for VesselWise, Google Fonts

---

## Inheritance Model

```
DESIGN.md (master)
  |
  |-- vesselwise-DESIGN.md   (overrides: VW brand colors, condition ratings,
  |                            D-DIN for standard codes, dark mode dashboard)
  |
  |-- fg-kpi-DESIGN.md       (overrides: IBM Plex Sans exclusively, Carbon
  |                            layer system, 0px radius buttons, 16-col grid,
  |                            risk heatmap + quality gauge components)
  |
  |-- wosa-docs-DESIGN.md    (overrides: ReportLab/PDF only, A4 page geometry,
                               no dark mode, cover page specs, photo evidence
                               layout, action tables, VW footer rules)
```

Where a variant file is silent on a topic, the master DESIGN.md rules apply.

---

## Design Sources

This system was built by analyzing and combining the best elements from:

| Source | What We Took | Grade |
|---|---|---|
| Stripe | Multi-layer shadow system, blue-tinted shadows, tabular numerals | A |
| Apple | Typography scale, negative letter-spacing, `#f5f5f7` surface | A |
| IBM Carbon | Semantic status tokens, 8px grid, Gray 100 dark theme, `0px` radius | A |
| Linear | Dark mode depth via luminance stepping, near-black canvas, cool grays | A |
| BMW | CSS custom property architecture, `--site-context-*` theming pattern | A- |
| Vercel | Metric card layout, shadow-as-border technique, data dashboard patterns | A |
| SpaceX | D-DIN typeface for technical classification headers | Reference |

---

## Quick Checklist

Before shipping any UI or document, verify:

- [ ] Colors come from CSS custom properties (or ReportLab constants), not hardcoded hex
- [ ] All numbers use IBM Plex Mono with `font-feature-settings: "tnum"`
- [ ] Spacing is on the 8px grid
- [ ] Status colors are semantic: red/amber/green/blue -- consistent everywhere
- [ ] No em dashes in any WOSA document
- [ ] Dark mode uses luminance stepping, not shadows
- [ ] Inter has negative letter-spacing at display sizes (>=32px)
- [ ] "Powered by VesselWise" follows the exact footer spec (7pt, #888888, greyscale icon)
