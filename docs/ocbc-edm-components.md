# OCBC EDM Component Library

## Global Rules
- **Never distort images.** Always use `background-size: 100% auto` or `background-size: contain` for background images, and `width: Xpx; height: auto` for `<img>` tags. Never set both width and height to fixed values that don't match the image's natural aspect ratio.

## Email Structure (top to bottom)

Every OCBC EDM follows this structure:
1. **Preview Liner** — single-line preview text
2. **Header** — OCBC logo + optional FNAB lockup
3. **Masthead + Intro** — hero background image + overlapping white intro card
4. **Content Sections** — modular white cards, each with eyebrow + title pattern
5. **Footer** — legal copy on off-white background

---

## 1. Preview Liner
- White background bar at the very top
- Desktop: py-10px px-30px, 10px Arial Regular, color #484848
- Mobile: py-10px px-30px, 10px Arial Regular, color #484848
- Contains short preview text visible in email client inbox

## 2. Header
### Desktop
- White background, h-98px, w-700px
- Left: Red brand band (7px wide, full height, #E30613) + OCBC logo (123x33px)
- Right: FNAB lockup logo (112.5x35px) — optional, depends on brand variant
- Brand variants: "OCBC", "OCBC with FNAB", "OCBC with FNAB CN"

### Mobile
- White background, h-67px, w-375px
- Left: Red brand band (4px wide) + OCBC logo (70.818x19px)
- Right: FNAB lockup (73.929x23px) — optional

## 3. Masthead + Intro (Overlapping Card)
The masthead and intro card are implemented as a **single container** using a CSS `background-image` technique. The intro card visually overlaps onto the bottom of the masthead hero image — it does NOT sit below it.

### Implementation Technique
- A single outer `<table>` has the masthead hero as `background-image` (not an `<img>` tag)
- The intro card is placed inside this container with `padding-top` to push it down so it partially overlaps the hero image
- The container has `background-color: #F7F8F9` so the area below the hero image blends with the page background

### Desktop (700px)
- Outer container: `background-image` with `background-size: 100% auto`, `background-repeat: no-repeat`, `background-position: top center`
- Container padding: `padding: 200px 45px 0 45px` — the 200px top padding positions the card so ~80px overlaps onto the hero
- Intro card: w-610px, `background-color: #FFFFFF`, centered

### Mobile (375px)
- Outer container: `background-image` with `background-size: 100% auto`
- Container padding: `padding: 140px 0 0 0` — the 140px top padding positions the card so ~56px overlaps onto the hero
- Intro card: full width (375px), `background-color: #FFFFFF`

### Intro Card Content
- **Headline**: Desktop 36px/38px Bold, Mobile 26px/28px Bold, color #484848, center-aligned
- **Body text**: 14px/20px Regular, color #484848, center-aligned
- **CTA**: "Book your FX rate now:" label + URL pill (URL in Geomanist 16px, h-30px, rounded-15px, bg white, border #CCCCCC)

## 4. Section Pattern (applies to ALL content sections)
Each section is a white card with:
- Desktop: px-30px pt-20px pb-30px (within the 45px outer container padding)
- Mobile: px-30px pt-20px pb-30px
- **Eyebrow line**: 50px wide, 2px tall, bg #484848
- **Section title**: 15px below eyebrow, 12px/20px Bold uppercase, tracking 3px, color #667C88
- **Content**: follows below the title

---

## Available Content Components

### A. Tables

#### Horizontal Table (standard)
- Full-width within section
- Header row: bg #667C88, white text, 14px Bold
- Data rows: white bg, #484848 text, 14px Regular
- Cell padding: Desktop 15px, Mobile 10px
- Borders: #EBEFF1 (desktop) or #F7F8F9 (mobile)
- Can highlight a row with bold text

#### Vertical Table (transposed)
- Left column = headers (bg #667C88, white text)
- Right column = data (white bg, #484848 text)
- Same border/padding pattern
- Can include "Blurb tag" badge (bg #39474E, white text, 10px Open Sans Bold, rounded-12px, px-10px py-3px)

### B. Icons + Description (vertical list)
- Each row: 100x100px icon centered above or beside text
- Desktop: icon left, text right, gap 30px, side by side
- Mobile: icon centered on top, text below, gap 20px
- Text: bold title (14px) + regular description (14px), color #484848

### C. Numbered List
- Each item: 40x40px circle (border #E6E4DF, 2px) with bold number (22px) + text
- Gap: Desktop 30px, Mobile 20px between circle and text
- Numbers are sequential (1, 2, 3...)
- Step 1 can include a URL pill link

### D. Benefits with Icons (3-column grid)
- Desktop: 3 columns, 170px each, gap 20px, side by side
- Mobile: 3 columns stacked or in a row (smaller)
- Each: 100x100px icon + bold title "Consectetur" + description text
- Icon-to-text gap: 20px

### E. Static Step-by-Step
- Has subtitle: "Non-animated step-by-step guide"
- Desktop: 3 steps, each with phone screenshot (350x279px) + "Step 0X" label + description
- Mobile: 3 steps, phone screenshot (260x207px) + label + description
- Gap between steps: 50px
- Italic note at bottom: "For illustration purposes only." (12px Italic)

### F. Animated Step-by-Step
Two sub-sections separated by OR Divider:

#### Via OCBC Digital app (Mobile Banking)
- Screenshot image (260x328px) + 3 numbered steps beside/below it
- Desktop: image left, steps right
- Mobile: image on top, steps below

#### OR Divider
- Horizontal line + "OR" circle (40x40px, bg #EAEAEA, text #999, 14px Bold) + horizontal line

#### Via OCBC Online Banking
- Carousel of screenshots (Desktop: 450px wide, Mobile: 315px wide) with dot indicator
- 3 numbered steps below
- Desktop: carousel left, steps right
- Mobile: carousel on top, steps below

### G. Excerpts/Quotes
- Body text introduction
- **Large quote**: 24px/30px Bold Italic, color #667C88, with opening/closing quotation marks
- More body text
- **Person quote block**: circular photo (110x110px) + italic quote (16px/22px #667C88) + name (bold) + title (regular), all #484848
- Desktop: photo and text side by side, gap 30px
- Mobile: photo centered on top, text below

### H. Testimonials
- Body text introduction
- **Testimonial block**: circular photo (110x110px) + attribution name (bold 14px) + italic quote (16px/22px #667C88) + person name (bold 14px)
- Desktop: photo left, text right, gap 30px
- Mobile: photo centered, text below, gap 15px
- More body text after

### I. Inline Images
Two variants:

#### Image on Right
- Text left, 150x150px circular image right
- Desktop: side by side
- Mobile: image centered on top, text below

#### Image on Left
- 150x150px circular image left, text right
- Desktop: side by side
- Mobile: image centered on top, text below

### J. Large Images
Two types:

#### Graph/Chart Image
- Full content width (Desktop: 550px, Mobile: 315px)
- Source caption below: italic 12px
- Body text follows

#### Banner Image
- Full content width (Desktop: 550x130px, Mobile: 315x74.455px)
- Body text follows

### K. Promo with Icon
- 100x100px giftbox icon + description text
- Desktop: icon left, text right, gap 30px
- Mobile: icon centered, text below, gap 20px

### L. Promo with Image
- Rectangular image (Desktop: 260x145px, Mobile: 315x175px) with silver (#CCCCCC) border
- Description text beside/below
- Desktop: image left, text right
- Mobile: image on top, text below

### M. Image with Play Button (Video)
- Same as Promo with Image but with dark overlay (rgba(0,0,0,0.7)) and 56x56px play button centered
- Indicates a video link

### N. Portfolio List
- 2x2 grid of portfolio items
- Each item: bold header + regular description (14px)
- Desktop: 2 columns side by side
- Mobile: 2 columns side by side (narrower)
- CTA at bottom: "Find out more:" + URL pill

## 5. Footer
- Background: #FAFCFC (off-white)
- Desktop: px-45px py-30px
- Mobile: p-30px
- Text: 12px/20px Regular, color #484848
- Content:
  1. Copyright line: "Copyright 2024 Oversea-Chinese Banking Corporation Limited. Co. Reg. No.: 193200032W"
  2. Contact info: Personal Banking hotline reference
  3. Marketing consent: Update preferences via OCBC Internet Banking
  4. Anti-phishing warning
