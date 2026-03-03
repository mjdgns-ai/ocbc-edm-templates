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
5. Claude critiques the draft copy, then rewrites to fix issues before finalising (see Copy Critique & Rewrite below)

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

## Copy Critique & Rewrite

**After generating the initial 3 HTML files, always perform a copy critique and produce rewritten v2 files.** This is a mandatory step in every EDM build. Act as a senior financial services copywriter (20+ years experience writing high-converting emails for banks) and evaluate the draft against the checklist below. Then save rewritten versions as `{product}-desktop-v2.html`, `{product}-mobile-v2.html`, and `{product}-responsive-v2.html`.

### Critique Checklist

1. **Preview liner / subject line hook** — Does it lead with a business problem or pain point, not a feature? Avoid product descriptions in preview text. Make the reader curious enough to open.

2. **Headline** — Is it anchored in a tangible business outcome? Avoid clever wordplay, puns, or rhymes that feel consumer-grade. Ensure the headline accurately describes what the product actually does (e.g. don't say "hedge" when most users do spot conversions).

3. **Intro body copy** — Does it get to the point in ≤2 sentences? Avoid worn-out openers ("Say hello to", "Introducing", "Meet the new"). Don't define acronyms the B2B audience already knows. Keep sentences under 25 words. State the problem, then the solution.

4. **Benefits** — Are they concrete and scenario-based, not abstract nouns? Each benefit title should describe a real user outcome (e.g. "See the exact rate before you commit") not a brand-deck abstraction (e.g. "Certainty"). Kill alliterative frameworks unless they earn their place.

5. **Repetition** — Does the email say the same value proposition more than twice? Every section should introduce new information or a new angle. If a section just restates what the intro already said, cut it or rewrite it with genuinely new content.

6. **How-to sections** — Is there only ONE how-to walkthrough? If the product works on multiple channels (web + app), lead with the primary channel and mention the secondary as a single line (e.g. "Prefer mobile? The same 3 steps work on the OCBC Business app."). Never show two full step-by-step walkthroughs — it doubles length and creates decision friction.

7. **Social proof / awards** — Are awards current and relevant to the audience? A retail award in a business banking email hurts credibility. Outdated awards (3+ years old) raise questions. If strong current proof isn't available, consider replacing with a usage stat or removing the section.

8. **CTA section** — Is there a single, clear call to action? Remove competing links (e.g. a "Learn more" URL pill next to a "Book now" button). Move secondary links to a P.S. line or footer. Every decision point is an exit point.

9. **Overall length** — Aim for 6-7 content sections max (not counting header/footer). An email should make one argument and ask for one action. More sections dilute rather than reinforce.

10. **Tone consistency** — Pick a lane: confident and direct for OCBC Business Banking. Not playful/casual, not stiff/corporate. Think: a knowledgeable banker who respects your time. Avoid mixing casual openers with institutional body copy.

### Rewrite Principles

- Lead with the business problem, not the product feature
- Use the verb "convert" for spot FX, not "trade" (which implies speculation)
- Benefits should answer: "What changes in my day-to-day operations?"
- One CTA per section, one primary action per email
- Shorter emails convert better in B2B — cut ruthlessly
- The "Learn more" product page link belongs in a P.S. or footer, not competing with the primary CTA
