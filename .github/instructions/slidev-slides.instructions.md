---
description: "Use when editing Slidev presentation files, writing slide content, or modifying slide styling and layouts."
applyTo: "{slides.md,pages/**/*.md}"
---

# Slidev Slide Conventions

## Slide Format
- Separate slides with `---`
- Per-slide frontmatter in YAML between `---` markers
- Speaker notes in `<!-- -->` at the end of each slide

## Design Rules — Speaker-First, Minimal Visuals
- **Maximum 7 words** of visible text per slide (code blocks excluded)
- **One idea per slide** — if there are two points, make two slides
- Prefer `layout: statement`, `center`, or `fact` over `default`
- Use blank/breathing slides between dense sections
- Speaker notes should contain the real narrative content
- Never use bullet-point lists on slides — split into individual slides instead

## Preferred Layouts
- `statement` / `center` — Single impactful line
- `fact` — A key number with a label
- `section` — Topic divider (just the section name)
- `image` — Full-bleed image, no text overlay
- `cover` — Title slide only
- `none` — Blank/breathing slide

## Animations
- Use `v-click` only for genuine reveals (max 3 per slide)
- Prefer `transition: fade` for reflective slides
- Use `transition: slide-left` for forward progression
- Keep transitions consistent within a section

## Styling
- UnoCSS utilities: `text-4xl`, `font-bold`, `op-80`, `text-center`
- Dark backgrounds (`bg-black text-white`) for dramatic emphasis
- Generous spacing (`mt-12`, `p-8`)
