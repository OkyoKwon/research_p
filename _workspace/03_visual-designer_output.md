# 크립토 결제 서비스 4종 비교 분석 -- Visual Design Specification

> PPTX Builder 에이전트가 python-pptx로 직접 구현 가능한 수준의 시각 사양서
> 작성일: 2026-04-15

---

## 1. Global Design System

### 1.1 Slide Dimensions

```
Width:  13.333 inches (Inches(13.333) or Emu(12192000))
Height: 7.5 inches   (Inches(7.5) or Emu(6858000))
Aspect: 16:9 widescreen
```

### 1.2 Color Palette

```python
# ── Backgrounds ──
BG_PRIMARY       = "#0F1923"   # Deep dark navy (main slide background)
BG_SECONDARY     = "#162033"   # Slightly lighter navy (content boxes)
BG_CARD          = "#1C2940"   # Card/panel background
BG_TABLE_HEADER  = "#2D2D44"   # Table header row
BG_TABLE_ROW_ODD = "#182338"   # Table odd rows
BG_TABLE_ROW_EVEN= "#1E2D45"   # Table even rows (alternating)
BG_TITLE_BAR     = "#0A1220"   # Title bar strip at top

# ── Text ──
TEXT_PRIMARY      = "#FFFFFF"   # Titles, headings, key numbers
TEXT_SECONDARY    = "#B8C4D4"   # Body text, descriptions
TEXT_TERTIARY     = "#7A8B9E"   # Captions, footnotes, sources
TEXT_DARK         = "#0F1923"   # Text on light/accent backgrounds

# ── Service Accent Colors ──
ACCENT_BASEPAY   = "#0052FF"   # Coinbase / Base blue
ACCENT_BINANCE   = "#F0B90B"   # Binance yellow
ACCENT_COINBASE  = "#1652F0"   # Coinbase Commerce blue (variant)
ACCENT_STRIPE    = "#635BFF"   # Stripe purple

# ── Semantic Colors ──
COLOR_POSITIVE    = "#00C853"   # Success, strengths, high score
COLOR_NEGATIVE    = "#FF5252"   # Warning, weaknesses, low score
COLOR_NEUTRAL     = "#FFD740"   # Neutral, medium, caution
COLOR_OPPORTUNITY = "#448AFF"   # Opportunity (SWOT)
COLOR_THREAT      = "#FF9100"   # Threat (SWOT)

# ── Priority Colors (for recommendations) ──
COLOR_P0          = "#FF5252"   # Critical / P0
COLOR_P1          = "#FF9100"   # High / P1
COLOR_P2          = "#FFD740"   # Medium / P2

# ── Confidence/Reliability ──
COLOR_HIGH_CONF   = "#00C853"   # 높음
COLOR_MED_CONF    = "#FFD740"   # 중
COLOR_LOW_CONF    = "#FF5252"   # 낮음

# ── Section Colors (for TOC and dividers) ──
SECTION_PART0     = "#78909C"   # 도입부 - blue grey
SECTION_PART1A    = "#0052FF"   # Base Pay
SECTION_PART1B    = "#F0B90B"   # Binance Pay
SECTION_PART1C    = "#1652F0"   # Coinbase Commerce
SECTION_PART1D    = "#635BFF"   # Stripe Crypto
SECTION_PART2     = "#26C6DA"   # 교차 비교 - cyan
SECTION_PART3     = "#AB47BC"   # 전략적 시사점 - purple
```

### 1.3 Typography

All fonts use "맑은 고딕" (Malgun Gothic). Fallback: "Arial".

```python
# ── Font Sizes (in Pt) ──
FONT_COVER_TITLE     = 36   # Cover slide title only
FONT_COVER_SUBTITLE  = 20   # Cover slide subtitle
FONT_SLIDE_TITLE     = 26   # Regular slide title
FONT_SECTION_TITLE   = 32   # Section divider title
FONT_SUBTITLE        = 18   # Slide subtitle / subheading
FONT_BODY            = 14   # Body text / bullets
FONT_BODY_SMALL      = 12   # Smaller body text (dense slides)
FONT_TABLE_HEADER    = 11   # Table header cells
FONT_TABLE_BODY      = 10   # Table body cells
FONT_TABLE_SMALL     = 9    # Compact tables (5+ columns)
FONT_CAPTION         = 9    # Footnotes, sources, captions
FONT_KPI_NUMBER      = 28   # Large KPI numbers
FONT_KPI_LABEL       = 10   # KPI labels below numbers

# ── Font Weights ──
# Title: Bold
# Subtitle: Bold
# Body: Regular
# Bold keywords: Bold within body text (use bold runs)
# Table header: Bold
# Table body: Regular
# Caption: Regular (italic for sources)
```

### 1.4 Common Elements

```python
# ── Slide Number ──
# Position: bottom-right
# x=12.2", y=7.1", w=1.0", h=0.3"
# Font: 9pt, TEXT_TERTIARY, right-aligned

# ── Confidential Footer ──
# Text: "내부 공유용 / Confidential"
# Position: bottom-left
# x=0.4", y=7.1", w=3.0", h=0.3"
# Font: 8pt, TEXT_TERTIARY, left-aligned

# ── Section Indicator Bar ──
# A thin horizontal line at the very top of each slide
# x=0", y=0", w=13.333", h=0.04"
# Color: varies by current section (see SECTION_* colors)
```

---

## 2. Layout Templates

All positions in inches (x, y, width, height) from top-left origin.

### 2.1 LAYOUT_COVER (표지)

```
┌─────────────────────────────────────────────────┐
│                                                   │
│                                                   │
│            [TITLE - centered, 36pt Bold]           │
│            [SUBTITLE - centered, 20pt]             │
│            [DATE + CONFIDENTIAL - 14pt]            │
│                                                   │
│           ═══════════════════════════              │
│           (accent line, 4 colors gradient)         │
│                                                   │
└─────────────────────────────────────────────────┘

Title box:       x=1.5,  y=1.8,  w=10.333, h=1.2
Subtitle box:    x=1.5,  y=3.2,  w=10.333, h=0.8
Accent line:     x=3.0,  y=4.3,  w=7.333,  h=0.06  (gradient or 4 segments)
  Segment 1:     x=3.0,  y=4.3,  w=1.833,  h=0.06  color=ACCENT_BASEPAY
  Segment 2:     x=4.833, y=4.3, w=1.833,  h=0.06  color=ACCENT_BINANCE
  Segment 3:     x=6.666, y=4.3, w=1.833,  h=0.06  color=ACCENT_COINBASE
  Segment 4:     x=8.499, y=4.3, w=1.834,  h=0.06  color=ACCENT_STRIPE
Body box:        x=1.5,  y=4.7,  w=10.333, h=1.5
  (Contains: 결제-정산-환불 line, date, confidential)
```

### 2.2 LAYOUT_TOC (목차)

```
┌─────────────────────────────────────────────────┐
│ [TITLE BAR]                                       │
│─────────────────────────────────────────────────│
│ ┌──LEFT COLUMN──┐   ┌──RIGHT COLUMN──────────┐  │
│ │ Part 0         │   │ #1~#8 -- Exec Summary  │  │
│ │ Part 1-A       │   │ #9~#20 -- Base Pay     │  │
│ │ Part 1-B       │   │ #21~#28 -- Binance Pay │  │
│ │ Part 1-C       │   │ #29~#36 -- Coinbase    │  │
│ │ Part 1-D       │   │ #37~#48 -- Stripe      │  │
│ │ Part 2         │   │ #49~#56 -- 교차 비교    │  │
│ │ Part 3         │   │ #57~#64 -- 결론         │  │
│ └────────────────┘   └────────────────────────┘  │
└─────────────────────────────────────────────────┘

Title bar:       x=0.4,  y=0.3,  w=12.533, h=0.7
Left column:     x=0.6,  y=1.3,  w=4.0,    h=5.5
Right column:    x=5.0,  y=1.3,  w=7.933,  h=5.5

Each TOC entry: left column has Part label with colored bullet (section color),
                right column has slide range and description.
Row height: ~0.65" each. Each Part label uses its section color for the text.
Vertical colored bar: x=4.8, y=1.3, w=0.04, h=5.5, color=TEXT_TERTIARY
```

### 2.3 LAYOUT_SECTION_DIVIDER (섹션 구분)

```
┌─────────────────────────────────────────────────┐
│ ┌──ACCENT BAR──┐                                 │
│ │              │                                 │
│ │   [PART #]   │      [SECTION TITLE]           │
│ │              │      [SUBTITLE/Description]     │
│ │              │                                 │
│ └──────────────┘                                 │
└─────────────────────────────────────────────────┘

Left accent bar: x=0,    y=0,    w=0.5,   h=7.5   (filled with section color)
Part label:      x=0.8,  y=2.5,  w=2.5,   h=0.6   (e.g., "Part 1-A")
  Font: 16pt, section color, Bold
Section title:   x=0.8,  y=3.2,  w=11.5,  h=1.2
  Font: 32pt, TEXT_PRIMARY, Bold
Subtitle:        x=0.8,  y=4.5,  w=11.5,  h=0.6
  Font: 16pt, TEXT_SECONDARY
Slide range:     x=0.8,  y=5.3,  w=11.5,  h=0.4
  Font: 12pt, TEXT_TERTIARY (e.g., "슬라이드 #9 ~ #20")
```

### 2.4 LAYOUT_TEXT (본문 텍스트)

```
┌─────────────────────────────────────────────────┐
│ ┌──TITLE BAR─────────────────────────────────┐  │
│ │ [SLIDE TITLE]                               │  │
│ └─────────────────────────────────────────────┘  │
│                                                   │
│  [BULLET CONTENT AREA]                            │
│  • Point 1                                        │
│  • Point 2                                        │
│  • Point 3                                        │
│                                                   │
│  [SOURCE/FOOTNOTE]                                │
└─────────────────────────────────────────────────┘

Title bar bg:    x=0,    y=0.15, w=13.333, h=0.85  color=BG_TITLE_BAR
Title text:      x=0.6,  y=0.2,  w=12.133, h=0.75
  Font: 26pt, TEXT_PRIMARY, Bold
Section color indicator: x=0, y=0.15, w=0.08, h=0.85  (thin left strip, section color)
Content area:    x=0.6,  y=1.3,  w=12.133, h=5.4
  Font: 14pt, TEXT_SECONDARY, line_spacing=1.4
Source box:      x=0.6,  y=6.85, w=12.133, h=0.25
  Font: 9pt, TEXT_TERTIARY, italic
```

### 2.5 LAYOUT_TEXT_4QUAD (4분할 텍스트) -- for Slide #3

```
┌─────────────────────────────────────────────────┐
│ [TITLE BAR]                                       │
│─────────────────────────────────────────────────│
│ ┌──QUAD 1 (BasePay)──┐ ┌──QUAD 2 (Binance)──┐  │
│ │ Blue accent top bar │ │ Yellow accent bar   │  │
│ │ Content...          │ │ Content...          │  │
│ └─────────────────────┘ └─────────────────────┘  │
│ ┌──QUAD 3 (Coinbase)─┐ ┌──QUAD 4 (Stripe)───┐  │
│ │ Blue variant bar    │ │ Purple accent bar   │  │
│ │ Content...          │ │ Content...          │  │
│ └─────────────────────┘ └─────────────────────┘  │
└─────────────────────────────────────────────────┘

Title bar: same as LAYOUT_TEXT
Quad 1 (top-left):     x=0.5,  y=1.3,  w=6.0,   h=2.8   bg=BG_CARD, border-top=ACCENT_BASEPAY(3pt)
Quad 2 (top-right):    x=6.8,  y=1.3,  w=6.0,   h=2.8   bg=BG_CARD, border-top=ACCENT_BINANCE(3pt)
Quad 3 (bottom-left):  x=0.5,  y=4.3,  w=6.0,   h=2.8   bg=BG_CARD, border-top=ACCENT_COINBASE(3pt)
Quad 4 (bottom-right): x=6.8,  y=4.3,  w=6.0,   h=2.8   bg=BG_CARD, border-top=ACCENT_STRIPE(3pt)

Each quad:
  Service label: top-left, 12pt, Bold, service accent color
  Content: 11pt, TEXT_SECONDARY, line_spacing=1.3
  Bold keyword highlight in service accent color
Gap between quads: 0.3" horizontal, 0.2" vertical
```

### 2.6 LAYOUT_TABLE (테이블)

```
┌─────────────────────────────────────────────────┐
│ [TITLE BAR]                                       │
│─────────────────────────────────────────────────│
│                                                   │
│  ┌──TABLE (full width)────────────────────────┐  │
│  │ HEADER ROW          (BG_TABLE_HEADER)       │  │
│  │ Row 1               (BG_TABLE_ROW_ODD)      │  │
│  │ Row 2               (BG_TABLE_ROW_EVEN)     │  │
│  │ Row 3               (BG_TABLE_ROW_ODD)      │  │
│  │ ...                                         │  │
│  └─────────────────────────────────────────────┘  │
│  [SOURCE/FOOTNOTE]                                │
└─────────────────────────────────────────────────┘

Title bar: same as LAYOUT_TEXT
Table area:      x=0.5,  y=1.3,  w=12.333, h=varies (auto)
Source box:      x=0.6,  y=6.85, w=12.133, h=0.25

Table styling:
  Header row bg: BG_TABLE_HEADER
  Header text: FONT_TABLE_HEADER, TEXT_PRIMARY, Bold, center-aligned
  Odd rows bg: BG_TABLE_ROW_ODD
  Even rows bg: BG_TABLE_ROW_EVEN
  Body text: FONT_TABLE_BODY, TEXT_SECONDARY, left-aligned (first col), center (others)
  Cell margins: top=0.04", bottom=0.04", left=0.08", right=0.08"
  Row height: 0.38" (standard), 0.32" (compact for large tables)
  Border: 0.5pt, color=#2A3A52 (subtle dark line), bottom border only for each row
  No outer border
```

### 2.7 LAYOUT_TABLE_COMPARISON (4서비스 비교 테이블)

Same as LAYOUT_TABLE but with column header coloring:

```
Column header colors (for 4-service comparison tables):
  Col 0 (항목): BG_TABLE_HEADER (default)
  Col 1 (Base Pay): #0052FF at 30% opacity overlay on BG_TABLE_HEADER → "#1A2E5A"
  Col 2 (Binance Pay): #F0B90B at 20% opacity overlay → "#3D3520"
  Col 3 (Coinbase Commerce): #1652F0 at 30% opacity → "#1A2E5A"
  Col 4 (Stripe Crypto): #635BFF at 30% opacity → "#2A2655"

  Implementation: Use these blended hex values directly:
    Col 1 header bg: "#1A2E5A"
    Col 2 header bg: "#3D3520"
    Col 3 header bg: "#1E2B55"
    Col 4 header bg: "#2A2655"
```

### 2.8 LAYOUT_TWO_COLUMN (2컬럼 비교)

```
┌─────────────────────────────────────────────────┐
│ [TITLE BAR]                                       │
│─────────────────────────────────────────────────│
│ ┌──LEFT (강점/긍정)──┐ ┌──RIGHT (약점/부정)──┐  │
│ │ Green top bar       │ │ Red top bar          │  │
│ │                     │ │                      │  │
│ │ • Item 1            │ │ • Item 1             │  │
│ │ • Item 2            │ │ • Item 2             │  │
│ │                     │ │                      │  │
│ └─────────────────────┘ └──────────────────────┘  │
│  [SOURCE/FOOTNOTE]                                │
└─────────────────────────────────────────────────┘

Title bar: same as LAYOUT_TEXT
Left column:     x=0.5,  y=1.3,  w=6.0,  h=5.3   bg=BG_CARD
  Top accent bar: x=0.5, y=1.3,  w=6.0,  h=0.06  color=COLOR_POSITIVE
  Column label:   "강점 / Strengths" or "호평" -- 14pt, Bold, COLOR_POSITIVE
Right column:    x=6.8,  y=1.3,  w=6.0,  h=5.3   bg=BG_CARD
  Top accent bar: x=6.8, y=1.3,  w=6.0,  h=0.06  color=COLOR_NEGATIVE
  Column label:   "약점 / Pain Points" -- 14pt, Bold, COLOR_NEGATIVE
Content font: 12pt, TEXT_SECONDARY, line_spacing=1.3
Gap: 0.3"
```

### 2.9 LAYOUT_DIAGRAM (다이어그램/플로우)

```
┌─────────────────────────────────────────────────┐
│ [TITLE BAR]                                       │
│─────────────────────────────────────────────────│
│                                                   │
│  ┌──DIAGRAM AREA──────────────────────────────┐  │
│  │                                             │  │
│  │  [Flowchart boxes / arrows / shapes]        │  │
│  │                                             │  │
│  └─────────────────────────────────────────────┘  │
│  [SOURCE/FOOTNOTE]                                │
└─────────────────────────────────────────────────┘

Title bar: same as LAYOUT_TEXT
Diagram area:    x=0.5,  y=1.3,  w=12.333, h=5.4

Flow step boxes:
  Size: 1.8" x 0.7" each
  Fill: BG_CARD
  Border: 1pt, service accent color
  Corner radius: 0.1"
  Text: 11pt, TEXT_PRIMARY, center-aligned
  Number badge: 0.3" circle, filled with accent color, white number

Arrow connectors:
  Color: TEXT_TERTIARY (#7A8B9E)
  Width: 1.5pt
  Style: solid with arrowhead

Vertical stack diagrams (for revenue layers, tech architecture):
  Layer boxes stacked vertically, each with left-color accent strip
```

### 2.10 LAYOUT_DIAGRAM_TABLE (다이어그램 + 테이블)

```
┌─────────────────────────────────────────────────┐
│ [TITLE BAR]                                       │
│─────────────────────────────────────────────────│
│  ┌──DIAGRAM (top)─────────────────────────────┐  │
│  │                                             │  │
│  │  [Flow / Diagram]                           │  │
│  └─────────────────────────────────────────────┘  │
│  ┌──TABLE (bottom)────────────────────────────┐  │
│  │ Header | Col1 | Col2 | Col3                │  │
│  │ ...                                         │  │
│  └─────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘

Title bar: same as LAYOUT_TEXT
Diagram area:    x=0.5,  y=1.3,  w=12.333, h=3.0
Table area:      x=0.5,  y=4.5,  w=12.333, h=2.5
```

### 2.11 LAYOUT_SWOT (2x2 SWOT 그리드)

```
┌─────────────────────────────────────────────────┐
│ [TITLE BAR]                                       │
│─────────────────────────────────────────────────│
│ ┌──S (green)──────────┐ ┌──W (red)─────────────┐│
│ │ Strengths            │ │ Weaknesses            ││
│ │ • item               │ │ • item                ││
│ │ • item               │ │ • item                ││
│ └──────────────────────┘ └───────────────────────┘│
│ ┌──O (blue)───────────┐ ┌──T (orange)───────────┐│
│ │ Opportunities        │ │ Threats               ││
│ │ • item               │ │ • item                ││
│ │ • item               │ │ • item                ││
│ └──────────────────────┘ └───────────────────────┘│
└─────────────────────────────────────────────────┘

Title bar: same as LAYOUT_TEXT

Strengths (top-left):
  Box: x=0.5,  y=1.3,  w=6.0,  h=2.7   bg=BG_CARD
  Top accent bar: x=0.5, y=1.3, w=6.0, h=0.06  color="#00C853" (green)
  Label: "Strengths (강점)", 13pt, Bold, "#00C853"

Weaknesses (top-right):
  Box: x=6.8,  y=1.3,  w=6.0,  h=2.7   bg=BG_CARD
  Top accent bar: x=6.8, y=1.3, w=6.0, h=0.06  color="#FF5252" (red)
  Label: "Weaknesses (약점)", 13pt, Bold, "#FF5252"

Opportunities (bottom-left):
  Box: x=0.5,  y=4.2,  w=6.0,  h=2.7   bg=BG_CARD
  Top accent bar: x=0.5, y=4.2, w=6.0, h=0.06  color="#448AFF" (blue)
  Label: "Opportunities (기회)", 13pt, Bold, "#448AFF"

Threats (bottom-right):
  Box: x=6.8,  y=4.2,  w=6.0,  h=2.7   bg=BG_CARD
  Top accent bar: x=6.8, y=4.2, w=6.0, h=0.06  color="#FF9100" (orange)
  Label: "Threats (위협)", 13pt, Bold, "#FF9100"

Content: 10pt, TEXT_SECONDARY, line_spacing=1.2
Gap: 0.3" horizontal, 0.2" vertical
```

### 2.12 LAYOUT_SUMMARY (요약)

```
┌─────────────────────────────────────────────────┐
│ [TITLE BAR]                                       │
│─────────────────────────────────────────────────│
│ ┌──KEY TAKEAWAY BOX───────────────────────────┐  │
│ │ ★ [Core message in bold, 16pt]               │  │
│ └──────────────────────────────────────────────┘  │
│                                                   │
│  [BULLET CONTENT AREA]                            │
│  1. Point 1                                       │
│  2. Point 2                                       │
│  ...                                              │
│  [SOURCE/FOOTNOTE]                                │
└─────────────────────────────────────────────────┘

Title bar: same as LAYOUT_TEXT
Key takeaway box: x=0.5, y=1.3, w=12.333, h=0.9
  bg: BG_CARD, left border 4pt accent color (section color)
  Text: 16pt, TEXT_PRIMARY, Bold
Content area:     x=0.5, y=2.5, w=12.333, h=4.3
  Text: 14pt, TEXT_SECONDARY
```

### 2.13 LAYOUT_KPI_CARDS (KPI 카드)

```
For slides with multiple KPI numbers (e.g., market data):

Row of 4 cards:
  Card 1: x=0.5,  y=1.3,  w=2.9,  h=1.5   bg=BG_CARD
  Card 2: x=3.65, y=1.3,  w=2.9,  h=1.5   bg=BG_CARD
  Card 3: x=6.8,  y=1.3,  w=2.9,  h=1.5   bg=BG_CARD
  Card 4: x=9.95, y=1.3,  w=2.9,  h=1.5   bg=BG_CARD

Each card:
  Top accent line: full width, h=0.04, accent color
  Number: centered, 28pt, Bold, TEXT_PRIMARY
  Label: centered, 10pt, TEXT_TERTIARY
  Bottom content area below cards for additional bullets
```

### 2.14 LAYOUT_TEXT_TABLE (텍스트 + 테이블)

```
┌─────────────────────────────────────────────────┐
│ [TITLE BAR]                                       │
│─────────────────────────────────────────────────│
│ ┌──TEXT (left)────────┐ ┌──TABLE (right)───────┐ │
│ │ Description text    │ │ Key | Value          │ │
│ │ ...                 │ │ ... | ...            │ │
│ └─────────────────────┘ └──────────────────────┘ │
└─────────────────────────────────────────────────┘

Title bar: same as LAYOUT_TEXT
Text area:   x=0.5,  y=1.3,  w=5.5,  h=5.4
Table area:  x=6.3,  y=1.3,  w=6.533, h=5.4
```

### 2.15 LAYOUT_DUAL_PANEL (듀얼 패널)

```
For side-by-side comparison of two concepts/products:

Title bar: same as LAYOUT_TEXT
Panel 1: x=0.5, y=1.3, w=6.0, h=5.3  bg=BG_CARD
Panel 2: x=6.8, y=1.3, w=6.0, h=5.3  bg=BG_CARD
Each panel has its own top accent bar (customizable color)
```

### 2.16 LAYOUT_TABLE_TIMELINE (테이블 + 타임라인)

```
Title bar: same as LAYOUT_TEXT
Table area:    x=0.5,  y=1.3,  w=12.333, h=3.0
Timeline area: x=0.5,  y=4.6,  w=12.333, h=2.3

Timeline: horizontal line with milestone markers
  Line: y=5.5, x=1.0 to x=12.0, 2pt, TEXT_TERTIARY
  Milestone circles: 0.2" diameter, filled with accent color
  Labels above/below alternating, 9pt
```

---

## 3. Slide-by-Slide Visual Specifications

### Part 0: 도입부 (Slides #1--#8)

Section color: `SECTION_PART0` (#78909C)

---

#### Slide #1: 표지
- **Layout**: LAYOUT_COVER
- **Background**: BG_PRIMARY
- **Special elements**:
  - Title: "크립토 결제 서비스 4종 심층 비교 분석" -- 36pt, Bold, TEXT_PRIMARY
  - Subtitle: "Base Pay / Binance Pay / Coinbase Commerce / Stripe Crypto" -- 20pt, TEXT_SECONDARY
  - 4-color accent line below subtitle (segments for each service accent color)
  - Body lines: "결제(Payment) - 정산(Settlement) - 환불(Refund) 전 과정 비교" -- 14pt, TEXT_SECONDARY
  - "작성일: 2026-04-15" -- 12pt, TEXT_TERTIARY
  - "내부 공유용 / Confidential" -- 12pt, TEXT_TERTIARY

---

#### Slide #2: 목차
- **Layout**: LAYOUT_TOC
- **Background**: BG_PRIMARY
- **Special elements**:
  - Each Part entry uses its section color for the bullet/marker
  - Part 0: #78909C | Part 1-A: #0052FF | Part 1-B: #F0B90B | Part 1-C: #1652F0 | Part 1-D: #635BFF | Part 2: #26C6DA | Part 3: #AB47BC
  - Slide range numbers in TEXT_TERTIARY
  - Active section indicator: small colored rectangle (0.15" x 0.15") before each Part label

---

#### Slide #3: Executive Summary -- 전체 핵심 인사이트
- **Layout**: LAYOUT_TEXT_4QUAD
- **Special elements**:
  - Quad 1 (top-left): Base Pay, top-border=ACCENT_BASEPAY
  - Quad 2 (top-right): Binance Pay, top-border=ACCENT_BINANCE
  - Quad 3 (bottom-left): Coinbase Commerce, top-border=ACCENT_COINBASE
  - Quad 4 (bottom-right): Stripe Crypto, top-border=ACCENT_STRIPE
  - Each quad: Service name in accent color, Bold
  - "약점:" prefix in COLOR_NEGATIVE within each quad
  - Key numbers in Bold TEXT_PRIMARY

---

#### Slide #4: Executive Summary -- 서비스별 한 줄 요약
- **Layout**: LAYOUT_TABLE
- **Table**: 4 columns (서비스, 핵심 포지션, 최대 강점, 최대 약점)
  - Column widths: 1.8", 3.5", 3.5", 3.5"
  - 서비스 column: Bold, service accent color for each service name
  - 최대 강점 column: text color=COLOR_POSITIVE (or TEXT_SECONDARY with green accent dot)
  - 최대 약점 column: text color=COLOR_NEGATIVE (or TEXT_SECONDARY with red accent dot)
  - Alternating row colors

---

#### Slide #5: 크립토 결제 시장 현황 개요
- **Layout**: LAYOUT_KPI_CARDS + body text below
- **Special elements**:
  - Top row: 4 KPI cards
    - Card 1: "$2.95B" / "결제 앱 시장 (2035)" / accent=#26C6DA
    - Card 2: "$4.74B" / "게이트웨이 시장 (2030)" / accent=#448AFF
    - Card 3: "$89.4B" / "스테이블코인 인프라 (2034)" / accent=#AB47BC
    - Card 4: "+43%" / "미국 결제 사용 증가" / accent=#00C853
  - Bottom section (y=3.1, h=3.5): additional bullet points
    - Font: 12pt, TEXT_SECONDARY
  - Source line at bottom

---

#### Slide #6: 5대 핵심 트렌드
- **Layout**: LAYOUT_DIAGRAM
- **Implementation**: 5 numbered boxes arranged vertically (stacked list style)
  - Each trend box: x=0.8, w=11.7, h=0.85
    - y positions: 1.3, 2.25, 3.2, 4.15, 5.1
    - Left number badge: 0.45" circle, filled #26C6DA, white number 18pt Bold
    - Box bg: BG_CARD
    - Title in Bold 13pt TEXT_PRIMARY, description in 11pt TEXT_SECONDARY
    - Left accent stripe (0.06" wide) in #26C6DA

---

#### Slide #7: 3대 진영 경쟁 구도
- **Layout**: LAYOUT_DIAGRAM
- **Implementation**: 3 large boxes (representing 3 camps)
  - Camp 1: x=0.5, y=1.3, w=3.9, h=4.5 -- bg=BG_CARD, top-accent=ACCENT_BINANCE
    - Label: "진영 1: 거래소 내장형"
    - Services listed inside
  - Camp 2: x=4.7, y=1.3, w=3.9, h=4.5 -- bg=BG_CARD, top-accent=#78909C
    - Label: "진영 2: 전통 게이트웨이형"
  - Camp 3: x=8.9, y=1.3, w=3.9, h=4.5 -- bg=BG_CARD, top-accent=ACCENT_STRIPE
    - Label: "진영 3: 전통 결제 확장형"
  - Bottom area (y=6.0): market share bar -- "BitPay 20% | CoinGate 14% | Coinbase 12% | Binance 8%"

---

#### Slide #8: 경쟁사 포지셔닝 맵
- **Layout**: LAYOUT_DIAGRAM
- **Implementation**: 2x2 matrix diagram
  - Axes drawn as lines with labels:
    - X-axis label: "법정화폐 통합도 →" (bottom, centered)
    - Y-axis label: "프로그래머빌리티 / 온체인 깊이 ↑" (left, rotated)
  - Quadrant labels (9pt, TEXT_TERTIARY):
    - Top-left: "프로그래머블 + 크립토 네이티브"
    - Top-right: "프로그래머블 + 법정화폐 통합" + "최대 위협 영역" badge in COLOR_NEGATIVE
    - Bottom-left: "단순 + 크립토 네이티브"
    - Bottom-right: "단순 + 법정화폐 통합"
  - Service bubbles (circles with service colors):
    - Base Pay: ACCENT_BASEPAY, top-left quadrant, r=0.35"
    - Binance Pay: ACCENT_BINANCE, bottom-left, r=0.45" (larger = more users)
    - Coinbase Commerce: ACCENT_COINBASE, center, r=0.3"
    - Stripe: ACCENT_STRIPE, top-right, r=0.4"
    - Additional smaller bubbles for BitPay, PayPal, Solana Pay in #78909C

---

### Part 1-A: Base Pay (Slides #9--#20)

Section color: `ACCENT_BASEPAY` (#0052FF)
Section divider slide is NOT numbered separately; slides #9-#20 are the content.

---

#### Slide #9: [Base Pay] 서비스 개요
- **Layout**: LAYOUT_TEXT_TABLE
- **Section indicator**: thin left strip on title bar = #0052FF
- **Left area**: Text description (definition, core value)
  - Service name "[Base Pay]" in ACCENT_BASEPAY Bold
- **Right area**: Key metrics table (2 columns: 항목, 내용)
  - Column widths: 2.0", 4.5"
  - 5 rows
  - Key numbers in Bold TEXT_PRIMARY

---

#### Slide #10: [Base Pay] 제품/프로토콜 라인업 및 타임라인
- **Layout**: LAYOUT_TABLE_TIMELINE
- **Table** (top): 4 columns (프로토콜, 세대, 핵심 기능, 배포 상태)
  - Column widths: 2.8", 1.5", 4.5", 3.5"
  - 4 rows, compact font (10pt)
- **Timeline** (bottom): horizontal with 5 milestones
  - Color: ACCENT_BASEPAY for milestone circles
  - Key dates: ~2024, 2025중반, 2025.09, 2026.02, 2026.03.31
  - "2026.03.31 Commerce 종료" milestone in COLOR_NEGATIVE

---

#### Slide #11: [Base Pay] 결제 시나리오 A: 즉시 결제 (Charge)
- **Layout**: LAYOUT_DIAGRAM_TABLE
- **Diagram (top)**: 6-step horizontal flow
  - Step boxes: 1.6" x 0.6", bg=BG_CARD, border=ACCENT_BASEPAY
  - Arrows between steps: #7A8B9E, 1.5pt
  - Final step highlight: border=COLOR_POSITIVE (success)
- **Table (bottom)**: 3 columns (항목, 금액, 부담 주체)
  - Column widths: 3.0", 4.0", 5.3"
  - 3 rows

---

#### Slide #12: [Base Pay] 결제 시나리오 B: 인가-캡처 결제
- **Layout**: LAYOUT_DIAGRAM_TABLE
- **Diagram (top)**: 6-step flow with "대기 기간" box highlighted in COLOR_NEUTRAL
  - "부분 캡처 지원" callout box: bg=BG_CARD, border=COLOR_POSITIVE, 10pt
- **Table (bottom)**: 4 columns (항목, 금액, 시점)
  - "Void 시 수수료 없음" cell: text in COLOR_POSITIVE

---

#### Slide #13: [Base Pay] x402 머신/AI 에이전트 결제
- **Layout**: LAYOUT_DIAGRAM_TABLE
- **Diagram (top)**: HTTP request-response sequence diagram (6 steps)
  - Client/Server columns
  - HTTP 402 response highlighted in COLOR_NEUTRAL
  - Final HTTP 200 in COLOR_POSITIVE
- **Table (bottom)**: x402 scheme comparison (exact vs upto)
  - 2 columns
- **Growth metrics**: small KPI bar at bottom-right
  - "1.19억+ 트랜잭션" "연간화 ~$600M" "USDC 98.7%"

---

#### Slide #14: [Base Pay] 지원 네트워크/토큰 및 통합 방식
- **Layout**: LAYOUT_TABLE (full)
- **Tables**: Two tables stacked
  - Table 1: Network support (4 columns, 3 rows) -- y=1.3, h=1.5
  - Table 2: Token Collector matrix (4 columns, 3 rows) -- y=3.2, h=1.5
  - Integration methods list below -- y=5.0, text bullets

---

#### Slide #15: [Base Pay] 정산 시나리오
- **Layout**: LAYOUT_DIAGRAM_TABLE
- **Diagram (top)**: Settlement flow paths (crypto direct vs fiat indirect)
  - Two parallel paths diverging from center
  - "법정화폐 전환" path: dotted line, COLOR_NEUTRAL annotation "추가 1-5 영업일"
- **Table (bottom)**: $100 cost simulation
  - Column widths: 4.0", 4.0", 4.3"
  - Highlight "법정화폐 직접 정산 미지원" in COLOR_NEGATIVE

---

#### Slide #16: [Base Pay] 환불 시나리오 (4가지)
- **Layout**: LAYOUT_TABLE
- **Table**: 4 columns (시나리오, 설명, 수수료, 속도)
  - Column widths: 2.5", 5.0", 2.5", 2.3"
  - 4 rows (A-D)
  - Scenario A "Void": highlight row with subtle green tint
  - Scenario C "Reclaim": highlight row with subtle blue tint (unique feature)
- **Below table**: State machine text "Created → Authorized → Captured/Voided/Reclaimed → Refunded"
  - Use arrow shapes, each state as a rounded rectangle

---

#### Slide #17: [Base Pay] 수익 구조 -- 5개 레이어
- **Layout**: LAYOUT_DIAGRAM
- **Implementation**: Stacked pyramid / layers (bottom = largest)
  - Layer 0 (bottom): w=11.0", h=0.85, bg="#0A2E6B" (dark blue), "$332.5M/분기"
  - Layer 1: w=9.5", h=0.85, bg="#0C3577", "$75.4M/년"
  - Layer 2: w=8.0", h=0.85, bg="#0E3C83"
  - Layer 3: w=6.5", h=0.85, bg="#104390", "1% 고정"
  - Layer 4 (top): w=5.0", h=0.85, bg="#12499D"
  - All centered horizontally. Labels on each layer in 11pt TEXT_PRIMARY
  - Left of each layer: Layer number badge

---

#### Slide #18: [Base Pay] 기술 아키텍처
- **Layout**: LAYOUT_DIAGRAM
- **Implementation**: Two-column architecture block diagram
  - Left column: "1세대 Transfers.sol" blocks
  - Right column: "2세대 AuthCaptureEscrow" blocks
  - Bottom: shared components (Solidity, Foundry, OpenZeppelin, x402)
  - Each block: rounded rect, bg=BG_CARD, border=ACCENT_BASEPAY
  - Security badge: "Spearbit 감사 완료" in COLOR_POSITIVE box

---

#### Slide #19: [Base Pay] 사용자 인사이트
- **Layout**: LAYOUT_TWO_COLUMN
- **Left column** (강점): green top bar, COLOR_POSITIVE label
  - 5 bullet points, each with green bullet marker
- **Right column** (약점): red top bar, COLOR_NEGATIVE label
  - 5 bullet points, severity tags [심각], [높음] in COLOR_NEGATIVE Bold
- **Bottom callout box** (below both columns):
  - x=0.5, y=6.0, w=12.333, h=0.7
  - bg=BG_CARD, left-border=COLOR_NEGATIVE 3pt
  - "시드 구문 보안 인시던트 (2026.03)" -- 11pt, COLOR_NEGATIVE Bold
  - "평점: Capterra 4.4/5, BBB F" in TEXT_TERTIARY

---

#### Slide #20: [Base Pay] SWOT 분석
- **Layout**: LAYOUT_SWOT
- **Colors**: S=green, W=red, O=blue, T=orange (as defined in template)
- **Content**: 10pt, each quadrant 4-5 bullet items
- **Special**: Bold keywords within each bullet

---

### Part 1-B: Binance Pay (Slides #21--#28)

Section color: `ACCENT_BINANCE` (#F0B90B)

---

#### Slide #21: [Binance Pay] 서비스 개요 및 핵심 수치
- **Layout**: LAYOUT_TEXT_TABLE
- **Left**: Service description, [Binance Pay] in ACCENT_BINANCE
- **Right**: KPI table (7 rows: 누적 거래량, 연간 거래량, etc.)
  - Column widths: 2.5", 4.0"
  - Key numbers Bold TEXT_PRIMARY
  - Asterisk footnote for 가맹점 수 (9pt, TEXT_TERTIARY)

---

#### Slide #22: [Binance Pay] 결제 시나리오 (4가지)
- **Layout**: LAYOUT_DIAGRAM
- **Implementation**: 4-panel grid (2x2)
  - Panel A: x=0.5, y=1.3, w=5.9, h=2.6 -- P2P
  - Panel B: x=6.7, y=1.3, w=5.9, h=2.6 -- Merchant Hosted
  - Panel C: x=0.5, y=4.1, w=5.9, h=2.6 -- Native API / Links
  - Panel D: x=6.7, y=4.1, w=5.9, h=2.6 -- QR Offline
  - Each panel: bg=BG_CARD, top-accent=ACCENT_BINANCE
  - Panel label: "시나리오 A" etc, 12pt Bold ACCENT_BINANCE
  - Content: 10pt TEXT_SECONDARY
  - Key numbers Bold

---

#### Slide #23: [Binance Pay] 수수료 구조
- **Layout**: LAYOUT_TABLE
- **Table**: 3 columns (수수료 항목, 요율, 비고)
  - Column widths: 3.5", 3.5", 5.3"
  - 6 rows
  - "FX 스프레드" row: bg tinted with COLOR_NEUTRAL at 15% opacity → use "#2A2820"
  - "0%" cells: COLOR_POSITIVE text
  - Below table: cost simulation box
    - bg=BG_CARD, "총비용: ~$140~150 (실효 ~1.4~1.5%)" in 14pt Bold TEXT_PRIMARY

---

#### Slide #24: [Binance Pay] 정산 시나리오
- **Layout**: LAYOUT_DIAGRAM_TABLE
- **Diagram (top)**: 4-step settlement flow (Binance internal ledger)
  - Steps connected by arrows, all within "Binance Ledger" container box
  - "즉시 입금" final step: COLOR_POSITIVE highlight
- **Table (bottom)**: Ledger performance (4 rows: TPS, 지연, 페일오버, 아키텍처)
  - "10,000+ TPS" and "10ms" in Bold COLOR_POSITIVE
- **Callout**: "법정화폐 전환 불가" box, COLOR_NEGATIVE left-border

---

#### Slide #25: [Binance Pay] 환불 시나리오
- **Layout**: LAYOUT_DIAGRAM_TABLE
- **Diagram (top)**: Refund flow (full/partial)
  - "환불 통화 불일치" callout in COLOR_NEUTRAL
- **Table (bottom)**: Error codes table (4 rows)
  - Column widths: 2.0", 10.3"

---

#### Slide #26: [Binance Pay] 비즈니스 모델 및 기술 아키텍처
- **Layout**: LAYOUT_DIAGRAM_TABLE
- **Table (top)**: Revenue structure (4 rows: MDR, Payout, FX, 생태계)
  - Column widths: 2.5", 5.0", 4.8"
  - "0.6%" highlighted in Bold, annotation "전략 도구"
- **Diagram (bottom)**: Tech stack blocks
  - Java/Spring Boot → Kafka → Redis → RocksDB
  - Horizontal flow, each as rounded rect with BG_CARD, border=ACCENT_BINANCE

---

#### Slide #27: [Binance Pay] 사용자 인사이트
- **Layout**: LAYOUT_TWO_COLUMN
- **Left** (호평): green top bar
  - 5 items (소비자 + 가맹점 positives)
- **Right** (불만): red top bar
  - Weighted score items: "고객 지원 (10/10)" etc.
  - Score numbers in COLOR_NEGATIVE Bold
- **Bottom callout**: "Trustpilot 1.4/5 vs App Store 4.7/5 -- 극단적 괴리"
  - bg=BG_CARD, border-left=COLOR_NEUTRAL

---

#### Slide #28: [Binance Pay] SWOT 분석
- **Layout**: LAYOUT_SWOT
- **Content**: per SWOT template

---

### Part 1-C: Coinbase Commerce (Slides #29--#36)

Section color: `ACCENT_COINBASE` (#1652F0)

---

#### Slide #29: [Coinbase Commerce] 서비스 개요
- **Layout**: LAYOUT_TEXT_TABLE
- **Left**: Description + "시장점유율 12% (3위)" highlighted
- **Right**: Product lineup timeline table (6 rows)
  - "2026.03.31 Commerce 종료" row: bg tinted with COLOR_NEGATIVE at 15% → "#2A1A1A"
- **Callout box** at bottom: "핵심 변곡점 -- 2026.03.31 Commerce 종료"
  - bg=BG_CARD, border-left=COLOR_NEGATIVE 4pt

---

#### Slide #30: [Coinbase Commerce] 결제 시나리오
- **Layout**: LAYOUT_DUAL_PANEL
- **Panel 1** (left): "기본 결제 (Charge)" -- top accent=ACCENT_COINBASE
  - 4 numbered steps
- **Panel 2** (right): "Protocol (Auth-Capture)" -- top accent=COLOR_POSITIVE
  - 4 steps: Authorize, Capture, Void, Reclaim
  - Each step name in Bold
- **Bottom bar**: supported coins and networks summary, 10pt

---

#### Slide #31: [Coinbase Commerce] 수수료 구조
- **Layout**: LAYOUT_TABLE
- **Table**: 4 columns (결제 유형, 수수료, 비고)
  - 4 rows
  - "무료" cells: COLOR_POSITIVE
  - Column widths: 3.5", 2.5", 6.3"
- **Below table**: Cost scenarios + comparison with Stripe/PayPal
  - "Stripe 카드 2.9%" and "PayPal 2.49%" in TEXT_TERTIARY for reference

---

#### Slide #32: [Coinbase Commerce] 정산 시나리오
- **Layout**: LAYOUT_TABLE + small diagram
- **Table**: Comparison table (Self-Managed vs Coinbase-Managed)
  - 4 columns: 항목, Self-Managed, Coinbase-Managed
  - Column widths: 2.5", 5.0", 5.0"
  - "불가" cells: COLOR_NEGATIVE
  - "가능" cells: COLOR_POSITIVE
- **Speed table** below (4 rows)

---

#### Slide #33: [Coinbase Commerce] 환불 시나리오
- **Layout**: LAYOUT_DIAGRAM_TABLE
- **Diagram (top)**: Three-path comparison (Self-Managed vs Managed vs Protocol)
  - Self-Managed path: COLOR_NEGATIVE dashed border ("수동")
  - Protocol path: COLOR_POSITIVE solid border
- **Callout**: "업계 최하위" badge in COLOR_NEGATIVE
  - x=9.0, y=5.5, w=3.8, h=0.6
  - bg=COLOR_NEGATIVE, text=TEXT_DARK, Bold 12pt

---

#### Slide #34: [Coinbase Commerce] 비즈니스 모델 및 기술
- **Layout**: LAYOUT_DIAGRAM_TABLE
- **Table (top)**: Revenue structure (5 rows)
- **Diagram (bottom)**: Vertical integration stack
  - Layers: 블록체인(Base) → 프로토콜 → 스테이블코인(USDC) → 지갑 → 거래소
  - "Visa 유사 모델" annotation

---

#### Slide #35: [Coinbase Commerce] 사용자 인사이트
- **Layout**: LAYOUT_TWO_COLUMN
- **Left**: Pain Points with severity x frequency scores
  - Each item: severity tag in colored badge [매우 높음]=red, [높음]=orange, [중간]=yellow
- **Right**: Additional pain points + platform ratings
- **Callout**: Security incident, COLOR_NEGATIVE border

---

#### Slide #36: [Coinbase Commerce] SWOT 분석
- **Layout**: LAYOUT_SWOT

---

### Part 1-D: Stripe Crypto (Slides #37--#48)

Section color: `ACCENT_STRIPE` (#635BFF)

---

#### Slide #37: [Stripe Crypto] 전략 전체상 및 수직 통합
- **Layout**: LAYOUT_DIAGRAM
- **Implementation**: 6-layer vertical stack (top to bottom = top of stack to bottom)
  - Each layer: full-width box, gradient from ACCENT_STRIPE at varying intensities
  - Layer 1 (Issuance): lightest purple bg
  - Layer 6 (Reserve): deepest purple bg
  - Each layer has: 레이어 label (left), 역할 (center), 기반 (right)
  - Font: 11pt per layer
- **Right side callout**: "구조적 해자 -- 아무도 복제 불가" in Bold 12pt
  - Rounded rect, border=ACCENT_STRIPE

---

#### Slide #38: [Stripe Crypto] 제품 포트폴리오 및 타임라인
- **Layout**: LAYOUT_TABLE_TIMELINE
- **Table (top)**: 3 columns (제품, 론칭, 핵심 기능), 8 rows
  - Column widths: 3.5", 2.0", 6.8"
  - Compact font: 9pt body
- **Timeline (bottom)**: Horizontal, 8+ milestones
  - "Bridge 인수 $1.1B" first milestone: larger circle, Bold annotation
  - Color: ACCENT_STRIPE

---

#### Slide #39: [Stripe Crypto] Stablecoin Payments
- **Layout**: LAYOUT_DIAGRAM_TABLE
- **Diagram (top)**: 5-step API flow
  - Code-style annotations (monospace for API calls)
  - "payment_intent.succeeded" in COLOR_POSITIVE
- **Table (bottom)**: Key specs (5 rows)
  - "업계 최초" cells: Bold, COLOR_POSITIVE
  - "미국 비즈니스만": COLOR_NEGATIVE

---

#### Slide #40: [Stripe Crypto] Pay with Crypto & Crypto Onramp
- **Layout**: LAYOUT_DUAL_PANEL
- **Panel 1**: Pay with Crypto (Crypto.com)
  - Top accent: ACCENT_STRIPE
- **Panel 2**: Crypto Onramp
  - Top accent: #26C6DA
- Each panel: 4-5 bullet points, key numbers in Bold

---

#### Slide #41: [Stripe Crypto] x402 & MPP
- **Layout**: LAYOUT_DIAGRAM_TABLE
- **Diagram (top)**: Side-by-side comparison visual
  - Left: x402 flow (3 steps) -- accent=ACCENT_BASEPAY
  - Right: MPP flow (3 steps) -- accent=ACCENT_STRIPE
- **Table (bottom)**: x402 vs MPP comparison (5 rows)
  - Column widths: 2.5", 5.0", 5.0"
  - "서브-100ms" in COLOR_POSITIVE Bold

---

#### Slide #42: [Stripe Crypto] 정산 시나리오
- **Layout**: LAYOUT_DIAGRAM
- **Implementation**: 4-stage pipeline (horizontal)
  - Stage 1: "온체인 수취" -- rounded rect, border=ACCENT_STRIPE
  - Stage 2: "Bridge 오케스트레이션" -- rounded rect
  - Stage 3: "Stripe 잔고 반영" -- rounded rect
  - Stage 4: "은행 출금 (T+2)" -- rounded rect, subtle COLOR_NEUTRAL border
  - Arrow connectors between stages
  - Time labels above each stage
- **Bottom callout**: "가맹점은 크립토를 전혀 보유하지 않음" in Bold 14pt, COLOR_POSITIVE
- **User feedback callout**: "T+2 정산 불만" in small box, COLOR_NEUTRAL

---

#### Slide #43: [Stripe Crypto] 수수료 구조 종합
- **Layout**: LAYOUT_TABLE
- **Table 1** (top): Product fees (5 rows, 3 cols)
  - Column widths: 3.5", 3.5", 5.3"
  - "1.5%" in Bold
  - "~5%" in COLOR_NEUTRAL
- **Table 2 / Bar area** (bottom): Monthly cost comparison
  - 5 services side-by-side (simulated bar chart using rectangles)
  - Each bar: width proportional to cost, height=0.4"
  - Stripe Stablecoin: ACCENT_STRIPE, "$150"
  - Stripe Card: #78909C, "$320"
  - Coinbase: ACCENT_COINBASE, "~$100+"
  - BitPay: #78909C, "~$125"
  - Binance: ACCENT_BINANCE, "~$180+"
  - Labels below each bar

---

#### Slide #44: [Stripe Crypto] 환불 시나리오
- **Layout**: LAYOUT_DIAGRAM_TABLE
- **Diagram (top)**: 4-step refund flow
  - "USD → 원래 스테이블코인 전환" step highlighted
- **Table (bottom)**: Key limitations (3 rows)
  - "미지원" and "불가" in COLOR_NEGATIVE
- **Callout**: "경쟁 공백 -- 온체인 분쟁 해결 선점 기회" in COLOR_OPPORTUNITY border box

---

#### Slide #45: [Stripe Crypto] Tempo 블록체인 핵심 사양
- **Layout**: LAYOUT_TABLE + diagram
- **Table** (left, x=0.5, w=6.0): 9 rows, 2 columns
  - "100,000+ TPS" in COLOR_POSITIVE Bold
  - "~0.6초" in COLOR_POSITIVE Bold
  - "없음" (네이티브 토큰) in COLOR_POSITIVE
  - "3곳" (검증자) in COLOR_NEUTRAL
- **Diagram** (right, x=6.8, w=6.0): simplified architecture block
  - Reth → Simplex BFT → Enshrined AMM
  - Partners: Visa, Zodia, Paradigm logos as text badges

---

#### Slide #46: [Stripe Crypto] 비즈니스 모델 및 파트너십
- **Layout**: LAYOUT_TABLE + diagram
- **Table (top, left)**: Revenue layers (7 rows)
  - "확인" confidence: COLOR_POSITIVE
  - "추정" confidence: COLOR_NEUTRAL
- **Diagram (bottom/right)**: Partner network
  - Central "Stripe" node (ACCENT_STRIPE circle)
  - Surrounding partner nodes connected by lines
  - 9 partners as smaller circles with labels

---

#### Slide #47: [Stripe Crypto] 사용자 인사이트
- **Layout**: LAYOUT_TWO_COLUMN
- **Left** (긍정): green top bar
  - Segment breakdown: 가맹점/개발자 55%, 소비자 40%
  - Shadeform case study: "66% 절감, 매출 10% 증가" in COLOR_POSITIVE Bold
- **Right** (부정): red top bar
  - "미국 전용" (가장 빈번) -- Bold, COLOR_NEGATIVE
  - "Tempo 반발" in COLOR_NEGATIVE
- **Bottom**: Improvement requests list (Top 5), numbered

---

#### Slide #48: [Stripe Crypto] SWOT 분석
- **Layout**: LAYOUT_SWOT

---

### Part 2: 교차 비교 분석 (Slides #49--#56)

Section color: `SECTION_PART2` (#26C6DA)

---

#### Slide #49: 수수료 비교 종합
- **Layout**: LAYOUT_TABLE_COMPARISON
- **Table**: 5 columns (항목 + 4 services), ~9 rows
  - Column widths: 2.3", 2.5", 2.5", 2.5", 2.5"
  - Compact font: 9pt body
  - Service column headers colored per service
  - Last two rows (총비용, 실효 수수료율): Bold, bg slightly lighter
  - Best value in each row: COLOR_POSITIVE
  - Worst value: COLOR_NEGATIVE
- **Below table**: Additional competitors in smaller text

---

#### Slide #50: 정산 비교 종합
- **Layout**: LAYOUT_TABLE_COMPARISON
- **Table**: 5 columns, 9 rows
  - Column widths: 2.3", 2.5", 2.5", 2.5", 2.5"
  - Compact font: 9pt
  - Highlight cells:
    - "직접" (Stripe 법정화폐 정산): COLOR_POSITIVE bg tint
    - "불가" (Binance 법정화폐): COLOR_NEGATIVE bg tint
    - "없음" (Stripe 크립토 노출): COLOR_POSITIVE bg tint
    - "온체인 지원" (에스크로): COLOR_POSITIVE text

---

#### Slide #51: 환불 비교 종합
- **Layout**: LAYOUT_TABLE_COMPARISON
- **Table**: 5 columns, 9 rows + comparison row
  - Column widths: 2.3", 2.5", 2.5", 2.5", 2.5"
  - "환불 UX 수준" last row:
    - "상" (Stripe): COLOR_POSITIVE bg, Bold
    - "중": COLOR_NEUTRAL bg
    - "하" (Coinbase): COLOR_NEGATIVE bg, Bold
  - "지원" cells: COLOR_POSITIVE text
  - "미지원" cells: COLOR_NEGATIVE text
  - "없음" (차지백): all cells same, COLOR_NEGATIVE

---

#### Slide #52: 기능 매트릭스 종합
- **Layout**: LAYOUT_TABLE_COMPARISON
- **Table**: 5 columns, 13 rows (LARGE TABLE)
  - Column widths: 2.0", 2.6", 2.6", 2.6", 2.5"
  - Very compact: 9pt body, 8pt if needed
  - Row height: 0.30"
  - Boolean-like cells: "지원" → checkmark-style green text, "미지원" → grey text
  - "업계 최초" annotations: COLOR_POSITIVE Bold
  - "예" (Binance 계정 필수): COLOR_NEGATIVE

---

#### Slide #53: 경쟁력 스코어카드 (10점 만점)
- **Layout**: LAYOUT_TABLE
- **Table**: 6 columns (항목 + 4 services + PayPal), 9 rows + total
  - Column widths: 2.0", 2.0", 2.0", 2.0", 2.0", 2.0"
  - Compact font: 10pt
  - Scores 8-10: COLOR_POSITIVE text
  - Scores 5-7: TEXT_PRIMARY
  - Scores 2-4: COLOR_NEGATIVE text
  - "종합" row: Bold, larger font (12pt)
  - Total row bg: slightly different (#1A2540)
  - Best score in each row: Bold + COLOR_POSITIVE

---

#### Slide #54: 비즈니스 모델 비교
- **Layout**: LAYOUT_TABLE_COMPARISON
- **Table**: 5 columns, 4 rows
  - Column widths: 2.0", 2.8", 2.8", 2.8", 2.8"
  - "0.6%" (Binance 전체 비중): Bold, COLOR_NEUTRAL
  - "Apache 2.0" (오픈소스): COLOR_POSITIVE text
  - "폐쇄적": COLOR_NEGATIVE text

---

#### Slide #55: 기술 아키텍처 비교
- **Layout**: LAYOUT_TABLE_COMPARISON
- **Table**: 5 columns, 7 rows
  - Column widths: 2.0", 2.8", 2.8", 2.8", 2.8"
  - Performance values Bold when best: "10,000+ TPS" (Binance), "100K+ TPS" (Stripe)
  - "Binance 앱만" in COLOR_NEGATIVE
  - "400+ 월렛" in COLOR_POSITIVE

---

#### Slide #56: 사용자 평점 및 Pain Points 비교
- **Layout**: LAYOUT_TABLE_COMPARISON
- **Table**: 5 columns, 5 rows
  - Column widths: 2.3", 2.5", 2.5", 2.5", 2.5"
  - Trustpilot scores: color-coded
    - 4.0+: COLOR_POSITIVE
    - 2.0-3.9: COLOR_NEUTRAL
    - <2.0: COLOR_NEGATIVE
  - Pain point cells: COLOR_NEGATIVE text for emphasis
- **Below table**: Common vs differential Pain Points summary
  - "공통: 고객 지원, 법정화폐 정산" in 12pt Bold
  - "차별적: Stripe만 고객 지원 불만 부재" in 12pt

---

### Part 3: 전략적 시사점 및 결론 (Slides #57--#64)

Section color: `SECTION_PART3` (#AB47BC)

---

#### Slide #57: AI 에이전트 결제 경쟁
- **Layout**: LAYOUT_TABLE + diagram
- **Table** (top): 6 protocols (6 rows, 4 columns)
  - Column widths: 2.0", 2.5", 3.5", 4.3"
  - Rows for x402, MPP, ACP highlighted with subtle color:
    - x402: ACCENT_BASEPAY tint
    - MPP: ACCENT_STRIPE tint
  - "4개 서비스 관계" column: Bold service names in their accent colors
- **Diagram** (bottom): Stripe's triple strategy visualization
  - Central "Stripe" node connected to x402, MPP, ACP
  - "어떤 표준이든 Stripe 존재" annotation

---

#### Slide #58: 시장 트렌드와 4개 서비스 대응 전략
- **Layout**: LAYOUT_TABLE_COMPARISON
- **Table**: 5 columns, 5 rows
  - Column widths: 2.3", 2.5", 2.5", 2.5", 2.5"
  - Color-coding per cell (대응 수준):
    - Strong response: COLOR_POSITIVE bg tint + Bold
    - Medium: COLOR_NEUTRAL bg tint
    - Weak/absent: COLOR_NEGATIVE bg tint ("미참여")
  - "자체가 전통 결제사": special highlight in ACCENT_STRIPE bg tint

---

#### Slide #59: 각 서비스 권고사항 종합
- **Layout**: LAYOUT_TABLE_COMPARISON
- **Table**: 5 columns, 6 rows
  - Column widths: 1.5", 2.7", 2.7", 2.7", 2.7"
  - Priority column color-coded:
    - "P0" rows: left-border 4pt COLOR_P0 (#FF5252)
    - "P1" rows: left-border 4pt COLOR_P1 (#FF9100)
    - "P2" rows: left-border 4pt COLOR_P2 (#FFD740)
  - Priority label Bold in respective color

---

#### Slide #60: 전략적 시사점 -- 5대 핵심 발견
- **Layout**: LAYOUT_TEXT (variant: numbered insights)
- **Implementation**: 5 numbered insight blocks stacked vertically
  - Each block: x=0.6, w=12.1, h=1.0
    - y positions: 1.3, 2.4, 3.5, 4.6, 5.7
    - Left number circle: 0.4" dia, filled SECTION_PART3, white number
    - Title in Bold 13pt TEXT_PRIMARY
    - Description in 11pt TEXT_SECONDARY
    - bg=BG_CARD for each block
    - Left accent stripe 0.04" in SECTION_PART3

---

#### Slide #61: 서비스별 최적 사용 시나리오
- **Layout**: LAYOUT_TABLE
- **Table**: 3 columns (시나리오, 최적 서비스, 근거)
  - Column widths: 3.5", 3.5", 5.3"
  - 10 rows
  - Compact font: 10pt
  - "최적 서비스" column: Bold, service accent color
  - Alternating row colors
  - "BitPay (4개 서비스 외)" in TEXT_TERTIARY italicized

---

#### Slide #62: 데이터 신뢰도 평가 종합
- **Layout**: LAYOUT_TABLE_COMPARISON
- **Table**: 5 columns, 7 rows
  - Column widths: 2.3", 2.5", 2.5", 2.5", 2.5"
  - Cell color-coding (reliability):
    - "높음": bg=COLOR_HIGH_CONF at 15% opacity → "#0F2520", text=COLOR_HIGH_CONF
    - "중-높": bg="#1A2520", text=COLOR_HIGH_CONF (slightly lighter)
    - "중": bg=COLOR_MED_CONF at 10% opacity → "#1F1F1A", text=COLOR_MED_CONF
    - "낮음": bg=COLOR_LOW_CONF at 10% opacity → "#1F1518", text=COLOR_LOW_CONF
  - Practical implementation hex values:
    - "높음" bg: "#122D1F"
    - "중-높" bg: "#1A2D22"
    - "중" bg: "#2A2A1A"

---

#### Slide #63: 결론 및 핵심 메시지
- **Layout**: LAYOUT_SUMMARY
- **Key takeaway box**: "크립토 결제는 기존 결제 인프라의 일부로 전환 중"
  - bg=BG_CARD, left-border=SECTION_PART3 4pt
  - 16pt Bold
- **Content area**: 5 numbered conclusions
  - Each conclusion: numbered, bold title + description
  - Key phrases in SECTION_PART3 color
  - 13pt for titles, 12pt for descriptions

---

#### Slide #64: 부록 -- 주요 출처 및 참고 자료
- **Layout**: LAYOUT_TEXT
- **Content**: Categorized source list
  - Category headers: 14pt, Bold, SECTION_PART3
  - Sources: 11pt, TEXT_TERTIARY
  - "분석 기준일: 2026-04-15" at bottom, Bold

---

## 4. Visual Elements Reference

### 4.1 Accent Bar Conventions

| Position | Width/Height | Usage |
|----------|-------------|-------|
| Top of slide | 13.333" x 0.04" | Section color indicator (all slides) |
| Left of title bar | 0.08" x 0.85" | Section color strip on title bar |
| Top of card/panel | varies x 0.06" | Card/panel accent bar |
| Left of callout | 0.04" x varies (4pt) | Callout box indicator |
| Left of section divider | 0.5" x 7.5" | Full-height section accent |

### 4.2 Table Cell Highlighting Rules

```python
# For comparison tables, apply these rules:

def get_cell_highlight(value_text, context):
    """Returns (bg_color, text_color) tuple or None for default."""

    # Best/positive values
    if value_text in ["지원", "직접", "가능", "무료", "없음(크립토 노출)"]:
        return (None, COLOR_POSITIVE)  # Green text only

    # Worst/negative values
    if value_text in ["미지원", "불가", "없음(차지백)", "제한적"]:
        return (None, COLOR_NEGATIVE)  # Red text only

    # UX level
    if value_text == "상":
        return ("#0F2520", COLOR_POSITIVE)
    if value_text == "하":
        return ("#2A1518", COLOR_NEGATIVE)
    if value_text == "중":
        return ("#2A2A1A", COLOR_NEUTRAL)

    # Scores (0-10)
    if value_text.isdigit():
        score = int(value_text)
        if score >= 8: return (None, COLOR_POSITIVE)
        if score <= 4: return (None, COLOR_NEGATIVE)

    return None  # Default styling
```

### 4.3 Table Column Width Presets

```python
# Standard 4-service comparison table
COLS_4SERVICE_STANDARD = [Inches(2.3), Inches(2.5), Inches(2.5), Inches(2.5), Inches(2.5)]

# Standard 4-service comparison table (with wider item column)
COLS_4SERVICE_WIDE = [Inches(2.8), Inches(2.4), Inches(2.4), Inches(2.4), Inches(2.4)]

# Standard 3-column detail table
COLS_3COL_DETAIL = [Inches(3.0), Inches(4.5), Inches(4.8)]

# Standard 2-column key-value table
COLS_2COL_KV = [Inches(3.0), Inches(9.3)]

# Compact 5-service table (with PayPal)
COLS_5SERVICE = [Inches(2.0), Inches(2.0), Inches(2.0), Inches(2.0), Inches(2.0), Inches(2.0)]
```

### 4.4 Service Name Formatting

Whenever a service name appears in body text or table cells, format with its accent color and Bold:

```python
SERVICE_FORMATS = {
    "Base Pay":           {"color": "#0052FF", "bold": True},
    "Binance Pay":        {"color": "#F0B90B", "bold": True},
    "Coinbase Commerce":  {"color": "#1652F0", "bold": True},
    "Stripe Crypto":      {"color": "#635BFF", "bold": True},
    "PayPal":             {"color": "#0070BA", "bold": True},
    "BitPay":             {"color": "#78909C", "bold": False},
}
```

### 4.5 Flow Diagram Step Box Specs

```python
FLOW_STEP_BOX = {
    "width": Inches(1.8),
    "height": Inches(0.7),
    "fill": BG_CARD,        # "#1C2940"
    "border_color": None,    # Set per-service accent
    "border_width": Pt(1),
    "corner_radius": Inches(0.1),
    "text_font_size": Pt(11),
    "text_color": TEXT_PRIMARY,
    "text_alignment": "center",
}

FLOW_ARROW = {
    "color": "#7A8B9E",
    "width": Pt(1.5),
    "head_type": "triangle",
}

FLOW_NUMBER_BADGE = {
    "diameter": Inches(0.3),
    "fill": None,           # Set per-service accent
    "text_color": "#FFFFFF",
    "text_font_size": Pt(10),
    "text_bold": True,
}
```

### 4.6 SWOT Grid Colors Summary

| Quadrant | Top Bar Color | Label Color | Content Theme |
|----------|--------------|-------------|---------------|
| Strengths (top-left) | #00C853 | #00C853 | Positive items |
| Weaknesses (top-right) | #FF5252 | #FF5252 | Negative items |
| Opportunities (bottom-left) | #448AFF | #448AFF | Future growth |
| Threats (bottom-right) | #FF9100 | #FF9100 | Risk items |

### 4.7 Slide Section Mapping

| Slide Range | Section Color | Part Label |
|-------------|--------------|------------|
| #1--#8 | #78909C | Part 0: 도입부 |
| #9--#20 | #0052FF | Part 1-A: Base Pay |
| #21--#28 | #F0B90B | Part 1-B: Binance Pay |
| #29--#36 | #1652F0 | Part 1-C: Coinbase Commerce |
| #37--#48 | #635BFF | Part 1-D: Stripe Crypto |
| #49--#56 | #26C6DA | Part 2: 교차 비교 |
| #57--#64 | #AB47BC | Part 3: 전략적 시사점 |

---

## 5. Slide-Layout Mapping (Quick Reference)

| Slide # | Title | Layout Template |
|---------|-------|-----------------|
| 1 | 표지 | LAYOUT_COVER |
| 2 | 목차 | LAYOUT_TOC |
| 3 | Executive Summary -- 핵심 인사이트 | LAYOUT_TEXT_4QUAD |
| 4 | Executive Summary -- 서비스별 요약 | LAYOUT_TABLE |
| 5 | 시장 현황 개요 | LAYOUT_KPI_CARDS |
| 6 | 5대 핵심 트렌드 | LAYOUT_DIAGRAM |
| 7 | 3대 진영 경쟁 구도 | LAYOUT_DIAGRAM |
| 8 | 경쟁사 포지셔닝 맵 | LAYOUT_DIAGRAM |
| 9 | [Base Pay] 서비스 개요 | LAYOUT_TEXT_TABLE |
| 10 | [Base Pay] 프로토콜 라인업 | LAYOUT_TABLE_TIMELINE |
| 11 | [Base Pay] 즉시 결제 | LAYOUT_DIAGRAM_TABLE |
| 12 | [Base Pay] 인가-캡처 결제 | LAYOUT_DIAGRAM_TABLE |
| 13 | [Base Pay] x402 머신 결제 | LAYOUT_DIAGRAM_TABLE |
| 14 | [Base Pay] 네트워크/토큰 | LAYOUT_TABLE |
| 15 | [Base Pay] 정산 시나리오 | LAYOUT_DIAGRAM_TABLE |
| 16 | [Base Pay] 환불 시나리오 | LAYOUT_TABLE |
| 17 | [Base Pay] 수익 구조 | LAYOUT_DIAGRAM |
| 18 | [Base Pay] 기술 아키텍처 | LAYOUT_DIAGRAM |
| 19 | [Base Pay] 사용자 인사이트 | LAYOUT_TWO_COLUMN |
| 20 | [Base Pay] SWOT | LAYOUT_SWOT |
| 21 | [Binance Pay] 서비스 개요 | LAYOUT_TEXT_TABLE |
| 22 | [Binance Pay] 결제 시나리오 | LAYOUT_DIAGRAM |
| 23 | [Binance Pay] 수수료 구조 | LAYOUT_TABLE |
| 24 | [Binance Pay] 정산 시나리오 | LAYOUT_DIAGRAM_TABLE |
| 25 | [Binance Pay] 환불 시나리오 | LAYOUT_DIAGRAM_TABLE |
| 26 | [Binance Pay] 비즈니스 모델 | LAYOUT_DIAGRAM_TABLE |
| 27 | [Binance Pay] 사용자 인사이트 | LAYOUT_TWO_COLUMN |
| 28 | [Binance Pay] SWOT | LAYOUT_SWOT |
| 29 | [Coinbase Commerce] 서비스 개요 | LAYOUT_TEXT_TABLE |
| 30 | [Coinbase Commerce] 결제 시나리오 | LAYOUT_DUAL_PANEL |
| 31 | [Coinbase Commerce] 수수료 구조 | LAYOUT_TABLE |
| 32 | [Coinbase Commerce] 정산 시나리오 | LAYOUT_TABLE |
| 33 | [Coinbase Commerce] 환불 시나리오 | LAYOUT_DIAGRAM_TABLE |
| 34 | [Coinbase Commerce] 비즈니스 모델 | LAYOUT_DIAGRAM_TABLE |
| 35 | [Coinbase Commerce] 사용자 인사이트 | LAYOUT_TWO_COLUMN |
| 36 | [Coinbase Commerce] SWOT | LAYOUT_SWOT |
| 37 | [Stripe Crypto] 전략 전체상 | LAYOUT_DIAGRAM |
| 38 | [Stripe Crypto] 제품 포트폴리오 | LAYOUT_TABLE_TIMELINE |
| 39 | [Stripe Crypto] Stablecoin Payments | LAYOUT_DIAGRAM_TABLE |
| 40 | [Stripe Crypto] Pay with Crypto & Onramp | LAYOUT_DUAL_PANEL |
| 41 | [Stripe Crypto] x402 & MPP | LAYOUT_DIAGRAM_TABLE |
| 42 | [Stripe Crypto] 정산 시나리오 | LAYOUT_DIAGRAM |
| 43 | [Stripe Crypto] 수수료 구조 | LAYOUT_TABLE |
| 44 | [Stripe Crypto] 환불 시나리오 | LAYOUT_DIAGRAM_TABLE |
| 45 | [Stripe Crypto] Tempo 블록체인 | LAYOUT_TABLE |
| 46 | [Stripe Crypto] 비즈니스 모델 | LAYOUT_TABLE |
| 47 | [Stripe Crypto] 사용자 인사이트 | LAYOUT_TWO_COLUMN |
| 48 | [Stripe Crypto] SWOT | LAYOUT_SWOT |
| 49 | 수수료 비교 종합 | LAYOUT_TABLE_COMPARISON |
| 50 | 정산 비교 종합 | LAYOUT_TABLE_COMPARISON |
| 51 | 환불 비교 종합 | LAYOUT_TABLE_COMPARISON |
| 52 | 기능 매트릭스 종합 | LAYOUT_TABLE_COMPARISON |
| 53 | 경쟁력 스코어카드 | LAYOUT_TABLE |
| 54 | 비즈니스 모델 비교 | LAYOUT_TABLE_COMPARISON |
| 55 | 기술 아키텍처 비교 | LAYOUT_TABLE_COMPARISON |
| 56 | 사용자 평점/Pain Points 비교 | LAYOUT_TABLE_COMPARISON |
| 57 | AI 에이전트 결제 경쟁 | LAYOUT_TABLE + diagram |
| 58 | 시장 트렌드 대응 전략 | LAYOUT_TABLE_COMPARISON |
| 59 | 권고사항 종합 | LAYOUT_TABLE_COMPARISON |
| 60 | 5대 핵심 발견 | LAYOUT_TEXT |
| 61 | 최적 사용 시나리오 | LAYOUT_TABLE |
| 62 | 데이터 신뢰도 평가 | LAYOUT_TABLE_COMPARISON |
| 63 | 결론 및 핵심 메시지 | LAYOUT_SUMMARY |
| 64 | 부록 -- 출처 | LAYOUT_TEXT |

---

*Visual Design Specification 작성 완료 -- 총 64장 슬라이드, 16개 레이아웃 템플릿*
