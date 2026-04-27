# Wawa Uiua Presentation

Slidev-based presentation about Uiua (a stack-based array programming language).

## Project Structure

- `slides.md` — Main presentation entry point (Slidev Markdown)
- `pages/` — Imported slide partials
- `components/` — Custom Vue components used in slides
- `snippets/` — Code snippets imported into slides
- `public/` — Static assets (images, icons)

## Build & Dev

```bash
npm run dev      # Start dev server with hot reload (opens browser)
npm run build    # Build static SPA for deployment
npm run export   # Export slides to PDF
```

## Slidev Conventions

- Slides separated by `---` in Markdown
- Per-slide config via YAML frontmatter (`layout`, `transition`, `class`, etc.)
- First frontmatter block = headmatter (deck-wide config: `theme`, `title`, `transition`)
- Speaker notes go in `<!-- ... -->` comment blocks at the end of each slide
- Vue components can be used inline in Markdown
- UnoCSS utility classes for styling
- Layouts: `cover`, `center`, `default`, `section`, `statement`, `fact`, `quote`, `image`, `image-left`, `image-right`, `two-cols`, `intro`, `end`, `none`
- Transitions: `fade`, `fade-out`, `slide-left`, `slide-right`, `slide-up`, `slide-down`, `view-transition`
- Click animations: `v-click`, `v-after`, `v-clicks`, `v-motion`

## Presentation Philosophy

This presentation follows a **speaker-first, minimal-visual** approach:
- Slides should be clean and uncluttered — the speaker carries the narrative
- Prefer blank/near-blank slides, single words, or evocative images over bullet-point walls
- Use `layout: statement` or `layout: center` for dramatic single-line messages
- Use `layout: fact` for key data points
- Emotional pacing matters — use empty space and timing to let ideas breathe
- Visuals should be separative (dividers between ideas), not decorative
- Never put on a slide what the speaker should say aloud

## Reference

- [Slidev Syntax Guide](https://sli.dev/guide/syntax)
- [Slidev Layouts](https://sli.dev/builtin/layouts)
- [Slidev Animations](https://sli.dev/guide/animations)
- [Slidev Components](https://sli.dev/builtin/components)
- [Slidev Directory Structure](https://sli.dev/custom/directory-structure)
