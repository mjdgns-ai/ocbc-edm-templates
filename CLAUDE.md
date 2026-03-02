# OCBC Bank EDM Template System

## Project Purpose
Create pixel-perfect OCBC Bank email campaigns (EDMs) from product/service website links using a component-based design system extracted from Figma.

## How It Works
1. User pastes a product/service website URL (e.g. `https://www.ocbc.com/business-banking/fx-online`)
2. Claude extracts content from the page: headlines, body copy, CTAs, images, key benefits, awards
3. Claude builds **3 HTML files** using OCBC EDM components:
   - `{product}-desktop.html` — fixed 700px width for desktop email clients
   - `{product}-mobile.html` — fixed 375px width for mobile email clients
   - `{product}-responsive.html` — single HTML with `@media (max-width: 480px)` breakpoints
4. All emails follow OCBC brand guidelines strictly

## Reference Files
- **Component library**: [docs/ocbc-edm-components.md](docs/ocbc-edm-components.md) — all available EDM components with specs
- **Design tokens**: [docs/ocbc-edm-tokens.md](docs/ocbc-edm-tokens.md) — colors, fonts, spacing values

## Figma Source (requires Figma MCP)
- File: `Global WEB - Design Language System` (key: `rScDtuLI0MiR81BIHTFRNK`)
- Desktop template node: `22724:30430`
- Mobile template node: `22724:29768`
- To connect: `claude mcp add --transport http figma-desktop http://127.0.0.1:3845/mcp`

## Example Output
The FX Online campaign files serve as reference implementations:
- [fx-online-desktop.html](fx-online-desktop.html) — desktop version (700px)
- [fx-online-mobile.html](fx-online-mobile.html) — mobile version (375px)
- [fx-online-responsive.html](fx-online-responsive.html) — responsive hybrid version

## Key Rules

### Layout
- Desktop width: 700px, content area: 550px (within 45px side padding + 30px section padding)
- Mobile width: 375px, content area: 315px (within 30px section padding)
- All sections are white cards on pale blue (#F7F8F9) background
- Gap between sections: 30px (`margin-bottom: 30px`)

### Structure (every EDM must have)
1. Preview liner — short preview text for inbox
2. Header — OCBC logo + red brand band + optional FNAB lockup
3. Masthead + Intro — hero image with overlapping white intro card
4. Content sections — modular white cards, each with eyebrow + title pattern
5. Footer — legal copy on off-white background

### Section Pattern
Every content section follows: eyebrow line (50px x 2px, #484848) → uppercase tracking title (12px, 3px letter-spacing, #667C88) → content

### Critical Design Rules
- **Masthead intro card MUST overlap** onto the hero image (use `background-image` container technique with `padding-top` — see component docs for exact values)
- **Never distort images**: for `<img>` tags use `height: auto` with explicit width only. For masthead background images, use `background-size: {width}px auto` (e.g. `700px auto` desktop, `375px auto` mobile) to maintain natural aspect ratio. Never hardcode both width and height.
- Font: Arial only (Regular 400, Bold 700, Bold Italic for quotes). Geomanist for URL pills only.
- Use table-based layouts for email compatibility (no `<div>`, no flexbox, no CSS grid)
- All styles must be inline (except `@media` queries in `<style>` for responsive version)
- Use `role="presentation"` on all layout tables
- Link color: #484848 for body links, #E30613 for red accent links

### Responsive HTML Rules
- Wrap everything in a `<style>` block with `@media only screen and (max-width: 480px)`
- Use CSS classes on table elements, then override with `!important` in media queries
- Key responsive behaviors: fluid widths, grid-to-stack, font size changes, padding adjustments
- Benefits grid → stacked single column on mobile
- Two-column content → stacked on mobile
- Desktop currency grid → inline bullet list on mobile

### Content Extraction
When building an EDM from a product page:
- Pull the hero/KV image from the product page
- Extract the main headline and adapt it for email (shorter, punchier)
- Summarize key benefits with their icons if available
- Include step-by-step guides if the product has a "how to" section
- Pull awards/accolades if present
- Ensure all links point to the real product page or Velocity login
- Use the product page URL as the "Learn more" CTA pill link

### Brand Assets (commonly used)
- OCBC Logo: `https://www.ocbc.com/iwov-resources/sg/ocbc/business/img/logo_ocbc.png`
- Product images are typically at: `https://www.ocbc.com/iwov-resources/sg/ocbc/business/img/{product}/`
