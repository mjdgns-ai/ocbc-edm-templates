# OCBC Bank EDM Template System

## Project Purpose
Create pixel-perfect OCBC Bank email campaigns (EDMs) from product/service website links using a component-based design system.

## Workflow
1. User pastes a product/service website link
2. Extract content (headlines, body copy, CTAs, images, key benefits)
3. Build desktop (700px) + mobile (375px) HTML emails using OCBC EDM components
4. All emails follow OCBC brand guidelines (Arial font, OCBC Red, blue-grey accents)

## Reference Files
- Component library: [docs/ocbc-edm-components.md](docs/ocbc-edm-components.md)
- Design tokens (colors, fonts, spacing): [docs/ocbc-edm-tokens.md](docs/ocbc-edm-tokens.md)

## Figma Source
- File: `Global WEB - Design Language System` (key: `rScDtuLI0MiR81BIHTFRNK`)
- Desktop template node: `22724:30430`
- Mobile template node: `22724:29768`

## Key Rules
- Desktop width: 700px, content area: 550px (within 45px side padding)
- Mobile width: 375px, content area: 315px (within 30px side padding)
- Font: Arial only (Regular 400, Bold 700, Bold Italic for quotes)
- Always include: Preview liner, Header, Masthead+Intro, Content sections, Footer
- Section pattern: eyebrow line (50px x 2px) + uppercase tracking title + content
- All sections are white cards on pale blue (#F7F8F9) background
- Masthead intro card must OVERLAP onto the hero image (use background-image container technique)
- **Never distort images**: use `background-size: 100% auto` for bg images, `height: auto` for img tags
