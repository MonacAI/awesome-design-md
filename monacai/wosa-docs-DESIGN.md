# WOSA Documents Design System

A PDF-focused design specification for all documents produced by WOSA Surveys: system annexes, meeting and visit reports, pre-purchase survey reports, monthly executive summaries, and formal correspondence. Generated via ReportLab. This document is a variant of the MonacAI master DESIGN.md, scoped exclusively to A4 PDF output.

**Scope:** ReportLab PDF generation only. No web, no slides, no dark mode. Every rule in this file takes precedence over the master DESIGN.md when working on WOSA documents.

---

## 1. Visual Theme and Atmosphere

WOSA documents communicate professional maritime authority, client confidence, and methodological rigour. The aesthetic is clean, conservative, and information-dense: white pages, controlled typographic hierarchy, two brand accent colours used purposefully, and zero decorative chrome.

**Registers by document type:**

| Document Type | Visual Register |
|---|---|
| System Annexes (FG, NEXT) | Formal and structured. Teal section bar headers, priority badges, photo evidence pages. Feels like a standards document. |
| Meeting / Visit Reports | Client-friendly and narrative. Red-ruled section headers, clean action tables. Feels like a professional report. |
| PPS Reports | Surveying authority. Neutral and factual. Same red-ruled headers as meeting reports. |
| Monthly Executive Summaries | Executive summary density. Maximum information in three pages. Mix of annex and report conventions. |

**Core principles:**
- Content is the hero. No decorative elements, no gradients, no textures, no clip art.
- Every colour use is semantic: red signals WOSA brand authority and action; teal signals structural categorisation; orange signals business risk; green signals compliance.
- Justified body text throughout. This is a formal document system, not a web interface.
- Whitespace is deliberate: consistent paragraph spacing, generous section spacing, tight caption spacing.
- Inter exclusively. No D-DIN, no monospace fonts, no serif type anywhere in these documents.

---

## 2. Color Palette and Roles

All colours are referenced by name and hex throughout this document. In ReportLab, always use `HexColor("...")` from `reportlab.lib.colors`.

### Brand Colours

| Role | Name | Hex | Usage |
|---|---|---|---|
| WOSA Red | `WOSA_RED` | `#A61B2B` | Section numbers (meeting reports), table headers, top accent bar, links, www.wosa.co.uk, cover type label, cover rule |
| WOSA Teal | `WOSA_TEAL` | `#1A6B6E` | Section header bars (annexes), sub-section headings (annexes), Supporting Evidence label, cover document title |

### Text Colours

| Role | Name | Hex | Usage |
|---|---|---|---|
| Dark text | `TEXT_DARK` | `#1C1C1C` | All body text, main headings |
| Light text | `TEXT_LIGHT` | `#555555` | Captions, metadata, secondary labels, version lines, company detail lines |
| Mid-grey | `TEXT_MID` | `#888888` | "Powered by VesselWise" text, tertiary labels |

### Surface and Border Colours

| Role | Name | Hex | Usage |
|---|---|---|---|
| Page background | `BG_WHITE` | `#FFFFFF` | All page backgrounds |
| Alternating row | `BG_ROW_ALT` | `#F5F5F5` | Table alternating rows, cover footer band |
| Border light | `BORDER_LIGHT` | `#D0D0D0` | Table borders, section rules, divider lines |
| Cover footer bg | `BG_COVER_FOOTER` | `#F5F5F5` | Cover page footer band |

### Status and Callout Colours

| Role | Name | Hex | Usage |
|---|---|---|---|
| Business Impact bg | `IMPACT_BG` | `#FFF8F0` | Business Impact callout box background |
| Business Impact border | `IMPACT_BORDER` | `#C8520A` | Left accent bar on Business Impact box |
| Business Impact text | `IMPACT_TEXT` | `#7A3000` | Business Impact label and body text |
| Priority 1 badge | `PRIORITY_1` | `#C8520A` | Priority badge in section headers (annexes) |
| Positive badge bg | `BADGE_POS_BG` | `#ECFDF5` | POSITIVE finding badge background |
| Positive badge text | `BADGE_POS_TEXT` | `#065F46` | POSITIVE finding badge text |
| Observation badge bg | `BADGE_OBS_BG` | `#FFFBEB` | OBSERVATION finding badge background |
| Observation badge text | `BADGE_OBS_TEXT` | `#92400E` | OBSERVATION finding badge text |
| Critical badge bg | `BADGE_CRIT_BG` | `#FEF2F2` | CRITICAL finding badge background |
| Critical badge text | `BADGE_CRIT_TEXT` | `#991B1B` | CRITICAL finding badge text |

### ReportLab Colour Constants

Define at the top of every build script:

```python
from reportlab.lib.colors import HexColor, white

WOSA_RED         = HexColor("#A61B2B")
WOSA_TEAL        = HexColor("#1A6B6E")
TEXT_DARK        = HexColor("#1C1C1C")
TEXT_LIGHT       = HexColor("#555555")
TEXT_MID         = HexColor("#888888")
BG_ROW_ALT       = HexColor("#F5F5F5")
BG_COVER_FOOTER  = HexColor("#F5F5F5")
BORDER_LIGHT     = HexColor("#D0D0D0")
IMPACT_BG        = HexColor("#FFF8F0")
IMPACT_BORDER    = HexColor("#C8520A")
IMPACT_TEXT      = HexColor("#7A3000")
PRIORITY_1       = HexColor("#C8520A")
BADGE_POS_BG     = HexColor("#ECFDF5")
BADGE_POS_TEXT   = HexColor("#065F46")
BADGE_OBS_BG     = HexColor("#FFFBEB")
BADGE_OBS_TEXT   = HexColor("#92400E")
BADGE_CRIT_BG    = HexColor("#FEF2F2")
BADGE_CRIT_TEXT  = HexColor("#991B1B")
```

---

## 3. Typography Rules

### Font Family

Inter exclusively. All weights are embedded TTF files loaded at document build time.

```python
from reportlab.pdfbase import pdfmetrics
from reportlab.pdfbase.ttfonts import TTFont

FONT_DIR = "/tmp/fonts"
pdfmetrics.registerFont(TTFont("Inter-Regular",   f"{FONT_DIR}/Inter-Regular.ttf"))
pdfmetrics.registerFont(TTFont("Inter-Light",     f"{FONT_DIR}/Inter-Light.ttf"))
pdfmetrics.registerFont(TTFont("Inter-Italic",    f"{FONT_DIR}/Inter-Italic.ttf"))
pdfmetrics.registerFont(TTFont("Inter-Medium",    f"{FONT_DIR}/Inter-Medium.ttf"))
pdfmetrics.registerFont(TTFont("Inter-SemiBold",  f"{FONT_DIR}/Inter-SemiBold.ttf"))
pdfmetrics.registerFont(TTFont("Inter-Bold",      f"{FONT_DIR}/Inter-Bold.ttf"))
```

No D-DIN. No IBM Plex Mono. No fallback to Helvetica unless fonts fail to load. Font loading failures must be caught and reported before generation begins.

### Type Scale

| Style | Font | Size | Leading | Alignment | Use |
|---|---|---|---|---|---|
| Cover title | Inter-Bold | 28pt | 34pt | Centred | Document title on cover page |
| Cover subtitle | Inter-Regular | 12pt | 16pt | Centred | Vessel/client/context on cover |
| Cover type label | Inter-SemiBold | 10pt | 13pt | Centred | "EXECUTIVE SYSTEM REPORT" etc. |
| Cover metadata | Inter-Medium / Inter-Regular | 9pt | 13pt | Centred | Version, date, description |
| Cover company | Inter-SemiBold / Inter-Regular | 7.5--8pt | 11pt | Left | Cover footer address block |
| Section header | Inter-Bold | 13pt | 16pt | Left | Primary section headings |
| Sub-section header | Inter-SemiBold | 10.5pt | 14pt | Left | 4.1 / 4.2 style headings |
| Body text | Inter-Regular | 9.5pt | 14pt | Justified | All body paragraphs |
| Body bold | Inter-SemiBold | 9.5pt | 14pt | Justified | Inline emphasis in body |
| Body italic | Inter-Italic | 9.5pt | 14pt | Justified | Observation openers, notes |
| Table header | Inter-SemiBold | 9pt | 12pt | Left | Table header row text |
| Table body | Inter-Regular | 9pt | 12pt | Left | Table cell body text |
| Caption | Inter-Italic | 8.5pt | 11pt | Left | Photo captions, figure labels |
| "Supporting Evidence" label | Inter-SemiBold | 11pt | 14pt | Left | Evidence section heading |
| Header company name | Inter-SemiBold | 8pt | 11pt | Right | Running header, company name line |
| Header detail lines | Inter-Regular | 7.5pt | 10pt | Right | Running header, address/VAT lines |
| Footer text | Inter-Regular | 6.5pt | 9pt | See footer spec | Running footer |
| VesselWise footer | Inter-Regular / Inter-Medium | 7pt | 9pt | Right | "Powered by VesselWise" |
| Prepared For label | Inter-Regular | 8pt | 11pt | Centred | "PREPARED FOR" label on cover |
| Prepared For name | Inter-Bold | 18pt | 22pt | Centred | Client name on cover |
| Prepared For location | Inter-Regular | 11pt | 14pt | Centred | Location on cover |

### Paragraph Styles (ReportLab ParagraphStyle)

```python
from reportlab.lib.styles import ParagraphStyle
from reportlab.lib.enums import TA_JUSTIFY, TA_LEFT, TA_CENTER, TA_RIGHT

body = ParagraphStyle(
    "body",
    fontName="Inter-Regular",
    fontSize=9.5,
    leading=14,
    alignment=TA_JUSTIFY,
    textColor=TEXT_DARK,
    spaceAfter=8,
)

body_bold = body.clone("body_bold", fontName="Inter-SemiBold")
body_italic = body.clone("body_italic", fontName="Inter-Italic")

caption = ParagraphStyle(
    "caption",
    fontName="Inter-Italic",
    fontSize=8.5,
    leading=11,
    alignment=TA_LEFT,
    textColor=TEXT_LIGHT,
    spaceAfter=4,
)

table_header_style = ParagraphStyle(
    "table_header",
    fontName="Inter-SemiBold",
    fontSize=9,
    leading=12,
    alignment=TA_LEFT,
    textColor=white,
)

table_body_style = ParagraphStyle(
    "table_body",
    fontName="Inter-Regular",
    fontSize=9,
    leading=12,
    alignment=TA_LEFT,
    textColor=TEXT_DARK,
)
```

### Typography Rules

1. Justified alignment on ALL body paragraphs. No exceptions.
2. No em dashes anywhere. See Section 7 (Hard Rules).
3. Paragraph spacing: 8pt after body paragraphs, 14pt before sub-section headers, 18pt before primary section headers, 6pt after sub-section headers.
4. No first-line indent on any paragraph.
5. Captions left-aligned and in Inter-Italic. Never justified.
6. Section headers and sub-section headers always left-aligned.
7. Cover page text always centred.

---

## 4. Document Components

### 4.1 Page Geometry (A4)

```python
from reportlab.lib.pagesizes import A4

PAGE_W, PAGE_H = A4      # 595.276 x 841.890 pt
MARGIN_LEFT   = 50
MARGIN_RIGHT  = 50
MARGIN_TOP    = 72       # content starts below fixed header
MARGIN_BOTTOM = 50

CONTENT_W = PAGE_W - MARGIN_LEFT - MARGIN_RIGHT   # 495.276 pt
```

### 4.2 Cover Page

The cover page is drawn entirely on the canvas inside the `Cover` page template callback. It does not use the story/flowable system. The running header callback must detect page 1 and skip (do not draw the running header on the cover).

**Visual structure (top to bottom):**

```
[thin WOSA Red bar — full page width, 6pt height, y = PAGE_H - 6]

[WOSA logo — centred, ~120pt wide]

[thin WOSA Red horizontal rule — full width between margins]

[spacer]

EXECUTIVE SYSTEM REPORT     ← Inter-SemiBold, 10pt, WOSA Red, centred
                             (or MEETING SUMMARY / VISIT REPORT / PRE-PURCHASE SURVEY)

[Document Title]             ← Inter-Bold, 28pt, WOSA Teal, centred, 2–3 lines max
[Subtitle line]              ← Inter-Regular, 12pt, TEXT_DARK, centred
Version 1.0, April 2026      ← Inter-Medium, 9pt, TEXT_LIGHT, centred
                               (omit on meeting reports and PPS reports)

[description paragraph — Inter-Regular, 9pt, TEXT_LIGHT, centred, up to 3 lines]

[thin divider — BORDER_LIGHT, 0.5pt]

PREPARED FOR                 ← Inter-Regular, 8pt, TEXT_LIGHT, centred, uppercase
Client Name                  ← Inter-Bold, 18pt, TEXT_DARK, centred
Location / Shipyard          ← Inter-Regular, 11pt, TEXT_LIGHT, centred

[distribution line — meeting reports only]
[status line (DRAFT / FINAL) — meeting reports only, when applicable]

[thin divider — BORDER_LIGHT, 0.5pt]

REFERENCE CAPTURE PERIOD     ← Inter-Regular, 8pt, TEXT_LIGHT, centred, uppercase
                               (or DATE OF VISIT / DATE OF SURVEY)
Date range / visit date      ← Inter-Regular, 12pt, TEXT_DARK, centred

[large white space]

[cover footer band — BG_COVER_FOOTER (#F5F5F5), ~80pt high, bottom of page]
  Wosa Surveys Sarl          ← Inter-SemiBold, 8pt, TEXT_DARK
  C/o CATS, 28 Bd Princesse Charlotte, 98000 Monaco (MC)  ← Inter-Regular, 7.5pt
  VAT FR34000151877  |  info@wosa.co.uk  ← Inter-Regular, 7.5pt
  www.wosa.co.uk             ← Inter-Regular, 7.5pt, WOSA Red
```

**Cover page variants by document type:**

| Field | System Annex | Meeting Report | PPS Report |
|---|---|---|---|
| Type label | EXECUTIVE SYSTEM REPORT | MEETING SUMMARY or VISIT REPORT | PRE-PURCHASE SURVEY |
| Title colour | WOSA Teal | WOSA Teal | WOSA Teal |
| Subtitle | "Installation Principles and Quality Control Guidelines" | Client and context | Vessel details (LOA, year, builder) |
| Version line | Show ("Version 1.0, April 2026") | Omit | Omit |
| Date block label | REFERENCE CAPTURE PERIOD | DATE OF VISIT | DATE OF SURVEY |
| Distribution line | Omit | Show | Omit |
| Status line | Omit | Show if DRAFT | Omit |
| "Prepared for" | Shipyard (e.g. Ferretti S.p.A.) | Client name | Client name |
| "Powered by VesselWise" | Never on cover | Never | Never |

### 4.3 Content Page Header

Fixed, drawn on every non-cover page. Implemented in the `Content` template's `onPage` callback.

```
[WOSA logo — left, ~55pt wide]        [Wosa Surveys Sarl — Inter-SemiBold, 8pt, right-aligned]
                                       [C/o CATS, 28 Bd Princesse Charlotte, 98000 Monaco (MC)]
                                       [VAT FR34000151877 | info@wosa.co.uk]
                                       [www.wosa.co.uk — WOSA Red]
──────────────────────────────────────────────────────────────  (BORDER_LIGHT, 0.5pt rule)
```

- Logo: left-aligned at `MARGIN_LEFT`, ~55pt wide, aspect-ratio preserved
- Company details: all lines right-anchored at `PAGE_W - MARGIN_RIGHT` using `drawRightString`
- "Wosa Surveys Sarl": Inter-SemiBold, 8pt, TEXT_DARK
- Address, VAT, email lines: Inter-Regular, 7.5pt, TEXT_LIGHT
- www.wosa.co.uk: Inter-Regular, 7.5pt, WOSA Red -- always in WOSA Red
- Horizontal rule: `y = PAGE_H - 60`, BORDER_LIGHT, 0.5pt
- The logo and company text must never overlap. Logo occupies the left ~25% of page width. Company details occupy the right half. Use `drawRightString` -- never `drawString` for the right-side block.

### 4.4 Content Page Footer

Fixed, drawn on every non-cover page alongside the header. Three-column layout.

```
CONFIDENTIAL          Page X          Grey Water System Annex  |  Ferretti S.p.A.  |  Ravenna
                                      Powered by VesselWise [icon]   ← qualifying documents only
```

- Left column: "CONFIDENTIAL" -- Inter-Regular, 6.5pt, TEXT_DARK, `drawString` at `MARGIN_LEFT`
- Centre column: "Page X" -- Inter-Regular, 6.5pt, TEXT_DARK, `drawCentredString` at `PAGE_W / 2`
- Right column: Document identifier string -- Inter-Regular, 6.5pt, TEXT_LIGHT, `drawRightString` at `PAGE_W - MARGIN_RIGHT`
- Footer baseline `y = 32`
- Document identifier format: `[Report Name]  |  [Client]  |  [Location]`
- Second footer line (right-aligned, `y = 21`): "Powered by VesselWise [icon]" only on qualifying documents (see Section 8)
  - "Powered by ": Inter-Regular, 7pt, TEXT_MID
  - "VesselWise": Inter-Medium, 7pt, TEXT_MID
  - VesselWise icon: 10pt height, aspect-ratio preserved, placed immediately right of "VesselWise" text

### 4.5 Section Headers

#### Primary Section Header -- Teal Bar (System Annexes)

Full-width teal background bar. Used in system annexes only.

```
┌──────────────────────────────────────────────────────────┬──────────────┐
│  4.  Section Title                   [white on teal bg]  │  PRIORITY 1  │
└──────────────────────────────────────────────────────────┴──────────────┘
```

- Bar background: WOSA Teal (`#1A6B6E`), full content width
- Bar height: 28pt, 8pt vertical padding
- Section number and title: Inter-Bold, 13pt, white
- Priority badge (right side): pill shape, `#C8520A` bg, white text, Inter-SemiBold, 8pt
  - "PRIORITY 1" for highest priority items
  - Teal-light (`#1A8C8F`) bg for Priority 2
- Space before: 18pt. Space after: 10pt.
- Implemented as a canvas drawing or as a custom Flowable that draws the bar then places text.

#### Primary Section Header -- Red-Ruled (Meeting Reports, PPS Reports)

No background bar. Clean numbered heading with a rule beneath.

```
1.  Section Title
────────────────────────────────────────────   (WOSA Red rule, full content width)
```

- Text: WOSA Red (`#A61B2B`), Inter-SemiBold, 13pt
- Rule: WOSA Red, 0.8pt linewidth, `CONTENT_W` span, 4pt below baseline
- Space before: 18pt. Space after: 10pt.

#### Sub-Section Header

For 4.1, 4.2 etc. style headings.

- System annexes: Inter-SemiBold, 10.5pt, WOSA Teal
- Meeting/PPS reports: Inter-SemiBold, 10.5pt, `#2C2C2C` (near-black)
- Space before: 14pt. Space after: 6pt.
- No rule below.

### 4.6 Business Impact Callout Box

Used in system annexes to flag commercial and operational risk.

```
┃  BUSINESS IMPACT                      ← Inter-SemiBold, 7pt, #C8520A, letter-spaced
┃  Body text explaining the impact...   ← Inter-Regular, 9pt, #7A3000
```

- Left border: 3pt, `#C8520A`
- Background: `#FFF8F0`
- Left padding: 10pt, right padding: 10pt, top/bottom padding: 8pt
- Label "BUSINESS IMPACT": Inter-SemiBold, 7pt, `#C8520A`, tracking approximately 1pt
- Body text: Inter-Regular, 9pt, `#7A3000`. Key phrases may be bolded using Inter-SemiBold.
- No em dashes in body text. Use commas, colons, or semicolons instead.
- Implemented as a Table with a coloured left border column (3pt wide, IMPACT_BORDER fill) and a text column.

```python
from reportlab.platypus import Table, TableStyle

def build_impact_box(label_text, body_text, styles):
    left_bar = Table([[""], [""]], colWidths=[3], rowHeights=[10, None])
    left_bar.setStyle(TableStyle([
        ("BACKGROUND", (0, 0), (-1, -1), IMPACT_BORDER),
        ("LINEABOVE", (0, 0), (-1, 0), 0, white),
    ]))
    label = Paragraph(label_text, styles["impact_label"])
    body  = Paragraph(body_text,  styles["impact_body"])
    content_col = [label, body]
    wrapper = Table([[left_bar, content_col]],
                    colWidths=[3, CONTENT_W - 3])
    wrapper.setStyle(TableStyle([
        ("BACKGROUND", (1, 0), (1, 0), IMPACT_BG),
        ("TOPPADDING",    (1, 0), (1, 0), 8),
        ("BOTTOMPADDING", (1, 0), (1, 0), 8),
        ("LEFTPADDING",   (1, 0), (1, 0), 10),
        ("RIGHTPADDING",  (1, 0), (1, 0), 10),
        ("VALIGN", (0, 0), (-1, -1), "TOP"),
    ]))
    return wrapper
```

### 4.7 Photo Evidence Layout (System Annexes)

- "Supporting Evidence" heading: Inter-SemiBold, 11pt, WOSA Teal, left-aligned
- Always wrap the heading and first photo row in `KeepTogether` to prevent orphaned headings
- Status badge above each photo: pill shape, correct badge colours (see status badges in Section 4.10)
- Caption text: Inter-Italic, 8.5pt, TEXT_LIGHT, left-aligned, directly below photo
- Caption must not contain em dashes

**3-photo header row layout:**
- Three equal-width columns within content width
- Each column: photo (landscape preferred) + status badge + caption
- Photo width: `(CONTENT_W - 12) / 3` (12pt total column gap)

**Single photo with context layout:**
- Photo: left column, ~45% of content width
- Badge + caption: right column, ~55% of content width
- Implemented as a 2-column `Table`

```python
from reportlab.platypus import KeepTogether, Image, Table, Paragraph

def build_evidence_section(photos):
    """photos: list of dicts with keys: path, status, caption"""
    elements = []
    heading = Paragraph("Supporting Evidence", styles["supporting_evidence"])

    # Build first row with heading kept together
    first_row = build_photo_row(photos[:3])
    elements.append(KeepTogether([heading, first_row]))

    # Additional rows without KeepTogether
    for i in range(3, len(photos), 3):
        elements.append(build_photo_row(photos[i:i+3]))
    return elements
```

### 4.8 Action Item Table

Used at the end of meeting reports and monthly executive summaries.

| # | Action | Owner | Priority |
|---|---|---|---|
| 1 | First action description | Responsible party | HIGH / MED / LOW |
| 2 | Second action | ... | ... |

- Header row: WOSA Red (`#A61B2B`) background, white Inter-SemiBold 9pt text
- Alternating body rows: white / `#F5F5F5`
- Body text: Inter-Regular, 9pt, TEXT_DARK
- Border: 0.5pt, BORDER_LIGHT (`#D0D0D0`)
- Row padding: 6pt vertical, 8pt horizontal
- Column widths (within CONTENT_W 495pt): `#` = 24pt, Action = 280pt, Owner = 110pt, Priority = 81pt
- **Action numbers always start at 1** regardless of document section or page number. This is a hard rule.
- Priority values: HIGH, MEDIUM, LOW -- never use em dashes as separators

```python
from reportlab.platypus import Table, TableStyle

def build_action_table(actions):
    """actions: list of dicts with keys: action, owner, priority"""
    header = ["#", "Action", "Owner", "Priority"]
    data = [header]
    for i, a in enumerate(actions, start=1):
        data.append([str(i), a["action"], a["owner"], a["priority"]])

    col_widths = [24, 280, 110, 81]
    t = Table(data, colWidths=col_widths)
    t.setStyle(TableStyle([
        # Header row
        ("BACKGROUND",    (0, 0), (-1, 0), WOSA_RED),
        ("TEXTCOLOR",     (0, 0), (-1, 0), white),
        ("FONTNAME",      (0, 0), (-1, 0), "Inter-SemiBold"),
        ("FONTSIZE",      (0, 0), (-1, 0), 9),
        ("TOPPADDING",    (0, 0), (-1, 0), 8),
        ("BOTTOMPADDING", (0, 0), (-1, 0), 8),
        ("LEFTPADDING",   (0, 0), (-1, 0), 8),
        # Body rows
        ("FONTNAME",      (0, 1), (-1, -1), "Inter-Regular"),
        ("FONTSIZE",      (0, 1), (-1, -1), 9),
        ("TOPPADDING",    (0, 1), (-1, -1), 6),
        ("BOTTOMPADDING", (0, 1), (-1, -1), 6),
        ("LEFTPADDING",   (0, 1), (-1, -1), 8),
        ("TEXTCOLOR",     (0, 1), (-1, -1), TEXT_DARK),
        ("ROWBACKGROUNDS",(0, 1), (-1, -1), [white, BG_ROW_ALT]),
        # Borders
        ("GRID",          (0, 0), (-1, -1), 0.5, BORDER_LIGHT),
        ("VALIGN",        (0, 0), (-1, -1), "TOP"),
    ]))
    return t
```

### 4.9 Standard Data Table

For structured data presented in system annexes, PPS reports, or meeting sections.

- Header row: WOSA Red (`#A61B2B`) background, white Inter-SemiBold 9pt
- Alternating rows: white / `#F5F5F5`
- Body text: Inter-Regular, 9pt, TEXT_DARK
- Border: 0.5pt, BORDER_LIGHT
- Row padding: 6pt vertical, 8pt horizontal
- Header padding: 8pt vertical, 8pt horizontal

```python
def standard_table_style():
    return TableStyle([
        ("BACKGROUND",    (0, 0), (-1, 0), WOSA_RED),
        ("TEXTCOLOR",     (0, 0), (-1, 0), white),
        ("FONTNAME",      (0, 0), (-1, 0), "Inter-SemiBold"),
        ("FONTSIZE",      (0, 0), (-1, 0), 9),
        ("TOPPADDING",    (0, 0), (-1, 0), 8),
        ("BOTTOMPADDING", (0, 0), (-1, 0), 8),
        ("LEFTPADDING",   (0, 0), (-1, -1), 8),
        ("FONTNAME",      (0, 1), (-1, -1), "Inter-Regular"),
        ("FONTSIZE",      (0, 1), (-1, -1), 9),
        ("TOPPADDING",    (0, 1), (-1, -1), 6),
        ("BOTTOMPADDING", (0, 1), (-1, -1), 6),
        ("TEXTCOLOR",     (0, 1), (-1, -1), TEXT_DARK),
        ("ROWBACKGROUNDS",(0, 1), (-1, -1), [white, BG_ROW_ALT]),
        ("GRID",          (0, 0), (-1, -1), 0.5, BORDER_LIGHT),
        ("VALIGN",        (0, 0), (-1, -1), "TOP"),
    ])
```

### 4.10 Status Badges

Used in photo evidence captions and finding summaries to classify the finding type.

| Badge | Background | Text colour | Font | Size |
|---|---|---|---|---|
| POSITIVE | `#ECFDF5` | `#065F46` | Inter-SemiBold | 7.5pt |
| OBSERVATION | `#FFFBEB` | `#92400E` | Inter-SemiBold | 7.5pt |
| CRITICAL | `#FEF2F2` | `#991B1B` | Inter-SemiBold | 7.5pt |

Badges are drawn on canvas as a rounded rectangle (radius 3pt) with text centred inside.

```python
def draw_badge(canvas_obj, x, y, label, bg_color, text_color,
               font="Inter-SemiBold", font_size=7.5, h=14, padding_x=8):
    text_w = canvas_obj.stringWidth(label, font, font_size)
    badge_w = text_w + padding_x * 2
    canvas_obj.setFillColor(bg_color)
    canvas_obj.roundRect(x, y, badge_w, h, radius=3, fill=1, stroke=0)
    canvas_obj.setFillColor(text_color)
    canvas_obj.setFont(font, font_size)
    canvas_obj.drawCentredString(x + badge_w / 2, y + (h - font_size) / 2, label)
    return badge_w  # return width so caller can position next element
```

---

## 5. Layout Principles

### 5.1 Spacing System

All vertical spacing is in points. These are fixed values, not a proportional grid.

| Token | Value | Use |
|---|---|---|
| `SP_PARA` | 8pt | Space after body paragraphs |
| `SP_CAPTION` | 4pt | Space after captions |
| `SP_SECTION_BEFORE` | 18pt | Space before primary section headers |
| `SP_SECTION_AFTER` | 10pt | Space after primary section headers |
| `SP_SUBSECTION_BEFORE` | 14pt | Space before sub-section headers |
| `SP_SUBSECTION_AFTER` | 6pt | Space after sub-section headers |
| `SP_PHOTO_ROW` | 8pt | Space between photo rows |
| `SP_TABLE_BEFORE` | 10pt | Space before a data table |
| `SP_TABLE_AFTER` | 12pt | Space after a data table |
| `SP_CALLOUT_BEFORE` | 10pt | Space before callout boxes |
| `SP_CALLOUT_AFTER` | 12pt | Space after callout boxes |

### 5.2 Content Flow

Documents use ReportLab's `BaseDocTemplate` with two `PageTemplate` instances:

1. **Cover template**: Single full-page `Frame` (no margins), `onPage = cover_page_handler`. Draws everything on canvas. Story contains only `NextPageTemplate("Content")` and `PageBreak()`.
2. **Content template**: `Frame` bounded by all four margins, `onPage = content_page_header_footer`. All document body flows through this frame as standard flowables.

```python
cover_frame = Frame(
    0, 0, PAGE_W, PAGE_H,
    leftPadding=0, rightPadding=0, topPadding=0, bottomPadding=0,
    id="cover"
)
content_frame = Frame(
    MARGIN_LEFT, MARGIN_BOTTOM,
    PAGE_W - MARGIN_LEFT - MARGIN_RIGHT,
    PAGE_H - MARGIN_TOP - MARGIN_BOTTOM,
    id="content"
)
```

### 5.3 Section and Content Sequencing

Standard section structure for system annexes:
1. Cover page (canvas-drawn, Cover template)
2. Report Contents / Table of Contents (first content page)
3. Introduction (italic paragraph, 2 paragraphs)
4. Section 1...N: section header, observation opener (italic), body text, sub-sections, Business Impact box, Supporting Evidence + photos

Standard structure for meeting reports:
1. Cover page
2. Purpose / Background
3. Attendees table
4. Positive Developments (bullet narrative)
5. Technical sections (numbered), each with context paragraph and "Requested action:" line
6. Action Register (action table)
7. Closing paragraph with contact details

### 5.4 Table of Contents Style

- "Report Contents" heading: Inter-Bold, 13pt, WOSA Red, left-aligned, with red rule beneath (same style as meeting report section headers)
- TOC entry: Inter-Regular, 9.5pt, TEXT_DARK, left-aligned
- TOC priority label: right-aligned on same line, Inter-SemiBold, 9pt, WOSA Teal or orange for Priority 1
- Dot leader between section title and priority label: Inter-Regular, 9pt, TEXT_LIGHT
- Space after TOC block: 18pt

---

## 6. Document Configuration and Asset References

### 6.1 Configuration Constants

Set at the top of every WOSA ReportLab build script:

```python
# Document identity
DOCUMENT_TITLE      = "Grey Water System"          # used in PDF metadata and cover
DOCUMENT_CLIENT     = "Ferretti S.p.A."
DOCUMENT_LOCATION   = "Ravenna"
DOCUMENT_IDENTIFIER = f"{DOCUMENT_TITLE} Annex  |  {DOCUMENT_CLIENT}  |  {DOCUMENT_LOCATION}"
INCLUDE_VW_FOOTER   = True   # False for meeting reports, PPS, proposals, client letters

# Asset paths
LOGO_PATH     = "/path/to/skills/user/wosa-branding/assets/logo-horizontal.jpg"
VW_ICON_PATH  = "/path/to/skills/user/vesselwise-branding/assets/VesselWise_Icon.png"
LOGO_ASPECT   = 4.0          # approximate width/height ratio of WOSA horizontal logo
VW_ICON_RATIO = 806 / 1284   # VesselWise icon width/height ratio

# Page geometry
PAGE_W, PAGE_H = A4
MARGIN_LEFT   = 50
MARGIN_RIGHT  = 50
MARGIN_TOP    = 72
MARGIN_BOTTOM = 50
CONTENT_W     = PAGE_W - MARGIN_LEFT - MARGIN_RIGHT
```

### 6.2 Company Details (Use Verbatim)

```
Wosa Surveys Sarl
C/o CATS, 28 Bd Princesse Charlotte, 98000 Monaco (MC)
VAT FR34000151877  |  info@wosa.co.uk
www.wosa.co.uk
```

VAT number must be present on all formal documents. Never omit it. The address and company name must match exactly -- "Wosa Surveys Sarl", not "WOSA Surveys", not "Wosa Surveys".

### 6.3 PDF Metadata

```python
doc = BaseDocTemplate(
    output_path,
    pagesize=A4,
    title=f"{DOCUMENT_TITLE}, {DOCUMENT_CLIENT}, {DOCUMENT_LOCATION}",
    author="Wosa Surveys Sarl",
    leftMargin=MARGIN_LEFT,
    rightMargin=MARGIN_RIGHT,
    topMargin=MARGIN_TOP,
    bottomMargin=MARGIN_BOTTOM,
)
```

Note: no em dashes in PDF metadata strings. Use commas to separate components.

---

## 7. Hard Rules

These rules apply to ALL document types without exception. Any violation is a formatting error.

1. **No em dashes anywhere.** Not in body text, not in captions, not in headers, not in metadata, not in Python string literals used for document content. Replace with: comma, colon, semicolon, or period as appropriate.

2. **Action item numbers always start at 1.** In any action table, number rows 1, 2, 3... regardless of what page or section the table falls on. Never use document-level counters or page numbers as action numbers.

3. **www.wosa.co.uk always in WOSA Red.** In both the running header and the cover footer. No exceptions.

4. **Cover page has no running header.** The `content_page_header_footer` callback must check `doc.page == 1` (or detect the Cover template) and exit without drawing. The cover page manages its own layout.

5. **"Powered by VesselWise" never appears on client-facing documents.** Not in the footer, not in the body, not in a watermark. See Section 8 for the full placement decision table.

6. **No VesselWise branding on PPS reports, meeting reports, proposals, or letters.** WOSA is acting as a client advisor or surveyor in these documents. VesselWise is not the relevant brand.

7. **VAT number always shown** on formal documents: `VAT FR34000151877`. Never omit.

8. **"Standardize" language is prohibited** in client-facing FG/NEXT documents. Use "It is recommended that FG review and align..." instead.

9. **Version number only on system annexes.** Format: "Version 1.0, April 2026" (comma separator, not em dash).

10. **Distribution list only on meeting reports.** Not on annexes, PPS reports, or summaries.

11. **Status line (DRAFT / FINAL) only on meeting reports** when the document is pending review. Not on annexes or PPS.

12. **No logo recreation.** Always use the provided logo image files. Never draw the WOSA wordmark in code or substitute plain text "WOSA" for the logo.

13. **Captions never contain em dashes.** Photo captions must use plain language with standard punctuation.

14. **Document metadata (PDF title/author) must not contain em dashes.**

---

## 8. VesselWise Footer Placement Rules

The "Powered by VesselWise" sub-footer line signals that VesselWise is the quality methodology platform underpinning the document. It appears only when WOSA is acting as a methodology or standards provider, never when WOSA is acting as a client advisor, surveyor, or correspondent.

| Document Type | Include "Powered by VesselWise"? | Reason |
|---|---|---|
| FG System Annexes | YES | Delivered to FG; VesselWise is the methodology platform |
| NEXT System Annexes | YES | Same as FG |
| Monthly Executive Summaries (FG, NEXT) | YES | Internal/semi-internal; methodology provenance relevant |
| Meeting / Visit Reports (client-facing) | NO | Pure WOSA client document; not a standards delivery |
| PPS Reports | NO | Client-facing survey report; surveyor identity only |
| VesselWise Construction Standards | YES | VesselWise is the primary brand on these documents |
| Proposals and Letters | NO | WOSA correspondent identity; no methodology reference |

Set `INCLUDE_VW_FOOTER = True` or `False` at the top of each build script. The header/footer callback reads this flag and draws (or omits) the second footer line accordingly.

---

## 9. Agent Prompt Guide

### Quick Reference -- Colours

| Name | Hex | Use |
|---|---|---|
| WOSA Red | `#A61B2B` | Section numbers (meeting reports), table headers, www.wosa.co.uk, cover rule, type label |
| WOSA Teal | `#1A6B6E` | Section bar headers (annexes), sub-section headings, supporting evidence label, cover title |
| Dark text | `#1C1C1C` | All body text, main headings |
| Light text | `#555555` | Captions, metadata, address lines |
| Business Impact left bar | `#C8520A` | Left border of Business Impact callout |
| Business Impact bg | `#FFF8F0` | Background of Business Impact callout |
| Business Impact text | `#7A3000` | Text inside Business Impact callout |
| POSITIVE badge bg | `#ECFDF5` | Status badge, positive findings |
| POSITIVE badge text | `#065F46` | Status badge, positive findings |
| OBSERVATION badge bg | `#FFFBEB` | Status badge, observations |
| CRITICAL badge bg | `#FEF2F2` | Status badge, critical findings |
| CRITICAL badge text | `#991B1B` | Status badge, critical findings |

### Quick Reference -- Fonts

All Inter. Sizes in points.

| Role | Font | Size | Leading |
|---|---|---|---|
| Cover title | Inter-Bold | 28 | 34 |
| Section header (bar) | Inter-Bold | 13 | 16 |
| Section header (ruled) | Inter-SemiBold | 13 | 16 |
| Sub-section header | Inter-SemiBold | 10.5 | 14 |
| Body | Inter-Regular | 9.5 | 14 |
| Table header | Inter-SemiBold | 9 | 12 |
| Table body | Inter-Regular | 9 | 12 |
| Caption | Inter-Italic | 8.5 | 11 |
| Footer | Inter-Regular | 6.5 | 9 |

### Component Prompt Templates

Use these prompts when instructing an agent to generate WOSA document elements:

---

**Cover page (system annex):**
> "Draw a WOSA system annex cover page on A4 canvas (595 x 842pt). Top bar: WOSA Red (#A61B2B), full width, 6pt. WOSA logo centred, 120pt wide. Thin red rule full width. Type label 'EXECUTIVE SYSTEM REPORT' centred, Inter-SemiBold 10pt, WOSA Red. Title centred, Inter-Bold 28pt, WOSA Teal (#1A6B6E). Subtitle centred, Inter-Regular 12pt, #1C1C1C. Version line centred, Inter-Medium 9pt, #555555. Thin divider BORDER_LIGHT (#D0D0D0), 0.5pt. 'PREPARED FOR' centred, Inter-Regular 8pt, #555555. Client name centred, Inter-Bold 18pt, #1C1C1C. Shipyard centred, Inter-Regular 11pt, #555555. Second divider. 'REFERENCE CAPTURE PERIOD' label. Date range, Inter-Regular 12pt. Cover footer band: #F5F5F5 bg, 80pt high at bottom. Company details from MARGIN_LEFT. www.wosa.co.uk in WOSA Red. No em dashes anywhere."

---

**Content page header:**
> "Draw WOSA running header on A4 content page. WOSA logo at left, 55pt wide, y = PAGE_H - 52. Company details right-aligned (drawRightString) at PAGE_W - 50: 'Wosa Surveys Sarl' Inter-SemiBold 8pt #1C1C1C; address line Inter-Regular 7.5pt #555555; VAT/email line Inter-Regular 7.5pt #555555; 'www.wosa.co.uk' Inter-Regular 7.5pt #A61B2B. Horizontal rule at y = PAGE_H - 60, BORDER_LIGHT (#D0D0D0), 0.5pt. Logo and text must not overlap."

---

**3-column footer:**
> "Draw WOSA 3-column footer at y=32. Left: 'CONFIDENTIAL' Inter-Regular 6.5pt #1C1C1C at MARGIN_LEFT. Centre: 'Page X' Inter-Regular 6.5pt #1C1C1C at PAGE_W/2 using drawCentredString. Right: document identifier string Inter-Regular 6.5pt #555555, drawRightString at PAGE_W - 50. If INCLUDE_VW_FOOTER is True, add 'Powered by VesselWise [icon]' at y=21, right-aligned, #888888, Inter-Regular + Inter-Medium 7pt."

---

**Section header bar (system annex):**
> "Draw WOSA teal section header bar. Rectangle from MARGIN_LEFT to PAGE_W - MARGIN_RIGHT, height 28pt, fill WOSA Teal (#1A6B6E). Section number and title in white Inter-Bold 13pt, left-aligned inside bar with 8pt left padding. If Priority 1: right-aligned pill badge in #C8520A background, white Inter-SemiBold 8pt text 'PRIORITY 1', 3pt radius, 8pt horizontal padding."

---

**Section header ruled (meeting report):**
> "Draw WOSA red-ruled section header. Text Inter-SemiBold 13pt WOSA Red (#A61B2B), left-aligned. Thin WOSA Red line (0.8pt) full content width (495pt) immediately below text, 4pt gap. Space before 18pt, space after 10pt."

---

**Business Impact callout box:**
> "Build Business Impact callout box, full content width. Left border column 3pt wide, fill #C8520A. Right column: background #FFF8F0, padding 8pt top/bottom, 10pt left/right. Label 'BUSINESS IMPACT' Inter-SemiBold 7pt #C8520A with letter-spacing. Body text Inter-Regular 9pt #7A3000. No em dashes."

---

**Action item table:**
> "Build WOSA action table. Columns: # (24pt), Action (280pt), Owner (110pt), Priority (81pt). Header row: WOSA Red (#A61B2B) bg, white Inter-SemiBold 9pt, 8pt padding. Body rows: alternating white/#F5F5F5, Inter-Regular 9pt #1C1C1C, 6pt vertical padding. 0.5pt BORDER_LIGHT (#D0D0D0) grid. Action numbers start at 1."

---

**Status badge:**
> "Draw status badge as a rounded rectangle (radius 3pt). POSITIVE: #ECFDF5 bg, #065F46 text. OBSERVATION: #FFFBEB bg, #92400E text. CRITICAL: #FEF2F2 bg, #991B1B text. Font: Inter-SemiBold 7.5pt. Horizontal padding: 8pt. Height: 14pt."

---

### Iteration Checklist for Agents

When generating or reviewing any WOSA document, verify:

1. No em dashes anywhere in the document (body, captions, headers, metadata)
2. www.wosa.co.uk is in WOSA Red (#A61B2B) in both header and cover footer
3. Action table numbers start at 1, not at any other value
4. "Powered by VesselWise" is present only on FG/NEXT annexes and monthly summaries
5. PPS reports and client-facing meeting reports have no VesselWise references anywhere
6. Cover page has no running header
7. Logo is the image file -- never a text substitute
8. VAT FR34000151877 appears in the cover footer and running header
9. All body text is justified (TA_JUSTIFY in ParagraphStyle)
10. Section header style matches the document type: teal bar for annexes, red-ruled for meeting/PPS
11. Sub-section headings are WOSA Teal in annexes, near-black in meeting/PPS reports
12. Version line present on annexes, absent on meeting reports and PPS
13. Distribution line present on meeting reports, absent elsewhere
14. Photo captions use Inter-Italic, contain no em dashes, have a status badge
15. Business Impact boxes use #FFF8F0 bg, #C8520A left bar, #7A3000 text -- no em dashes
