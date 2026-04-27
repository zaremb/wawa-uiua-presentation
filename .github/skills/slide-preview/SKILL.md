---
name: slide-preview
description: "Preview and visually inspect Slidev slides using headless export or Playwright browser. Use when checking slide rendering, taking screenshots, reviewing visual quality, navigating the presentation, or debugging visual issues with slides."
---

# Slide Preview & Visual Inspection

Visually inspect rendered Slidev slides by exporting them as PNG images (preferred) or via Playwright MCP browser tools.

## Method 1: Headless PNG Export (Preferred)

This is the most reliable method — works in WSL, CI, and headless environments without browser display issues.

### Prerequisites

```bash
npm i -D playwright-chromium   # One-time: adds headless Chromium for export
sudo npx playwright install-deps  # One-time: installs system libs (needs sudo)
```

### Export All Slides as PNGs

```bash
npx slidev export --format png --output slides-export --dark 2>&1
```

This creates `slides-export/` with one PNG per slide: `001.png`, `002.png`, etc.

### View the Exported Images

Use the `view_image` tool to inspect each PNG:
```
view_image("slides-export/001.png")
```

### CRITICAL: Image Limit Per Request

**The model supports a maximum of 20 images per request.**

If the presentation has more than 20 slides:
- **Batch reviews**: Inspect slides 1-15 in one pass, then 16+ in the next
- **Prioritize**: Review section openers, code slides, and the title/close slides first
- **Skip blanks**: Slides with `layout: none` or pure black backgrounds don't need visual review
- Count PNGs first: `ls slides-export/*.png | wc -l`

### Re-export After Changes

After fixing visual issues, re-export to verify:
```bash
rm -rf slides-export && npx slidev export --format png --output slides-export --dark 2>&1
```

## Method 2: Playwright MCP Browser (Interactive)

Use when you need to interact with slides (click animations, test transitions) or when the Playwright MCP browser tools are available and working.

### Known Issues in WSL

- The Playwright MCP extension runs on the **Windows host**, not inside WSL
- Windows Chrome may block with "DevTools remote debugging disallowed by system admin" — this is a Windows Group Policy issue, not fixable from WSL
- If the MCP browser fails to launch, **fall back to Method 1** (headless export)

### If MCP Browser Works

1. Ensure dev server is running: `npm run dev` (default: `http://localhost:3030`)
2. Navigate: `mcp_microsoft_pla_browser_navigate` to `http://localhost:3030/{slideNumber}`
3. Screenshot: `mcp_microsoft_pla_browser_take_screenshot`
4. Navigate between slides: `mcp_microsoft_pla_browser_press_key` with `ArrowRight`/`ArrowLeft`
5. Inspect DOM: `mcp_microsoft_pla_browser_snapshot` for accessibility tree

## Review Checklist

When inspecting each slide visually, check:

### Layout & Spacing
- [ ] Content is vertically centered (not bunched at top)
- [ ] Generous whitespace around all elements
- [ ] Text doesn't overflow or get cut off
- [ ] Images are properly sized and not stretched

### Typography
- [ ] Text is large enough to read at distance (min `text-2xl`)
- [ ] Font rendering is clean (mono fonts for code, sans for prose)
- [ ] Opacity/color contrast is sufficient against background

### Consistency
- [ ] Dark background is consistent across slides (no flashing white)
- [ ] Font sizes match between similar slide types
- [ ] Color accent usage is consistent (e.g., green for Uiua glyphs)

### Content
- [ ] One idea per slide — no visual clutter
- [ ] Code blocks render with syntax highlighting
- [ ] Images load correctly (no broken image icons)
- [ ] v-click elements are hidden by default (only visible after click)
