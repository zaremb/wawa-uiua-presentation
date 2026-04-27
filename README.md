# Wawa-Uiua! Very Nice Array Programming! 🍕

> A 10-minute lightning talk about [Uiua](https://www.uiua.org/) — a stack-based array programming language that looks like someone spilled a Unicode chart on their keyboard.

Presented at **Python Pizza Warsaw** by [Mateusz Zaremba](https://www.linkedin.com/in/mateusz-zaremba/).

## What's this about?

Uiua (pronounced "WEE-wah") is a language where a single line like:

```
/+×2▽=0◿2⟜∘⇡10
```

filters even numbers, doubles them, and sums the result — no variables, no loops, no names.

This talk introduces Uiua through the lens of a Python developer, showing how array thinking can change the way you write code.

## Running locally

```bash
npm install
npm run dev        # starts dev server at http://localhost:3030
```

## Building & exporting

```bash
npm run build      # build static SPA
npm run export     # export slides to PDF (requires playwright-chromium)
```

## Project structure

```
slides.md           # main entry point (Slidev markdown)
pages/              # slide sections
  01-the-hook.md    # opening — Klingon + Uiua reveal
  02-concepts.md    # stack & array fundamentals
  03-demo.md        # Python vs Uiua side-by-side
  04-the-why.md     # why should Pythonistas care
  05-close.md       # closing
  06-backup.md      # bonus Fibonacci deep-dive
components/         # custom Vue components (BgEmoji, etc.)
style.css           # global styles
```

## Built with

- [Slidev](https://sli.dev/) — presentation slides for developers
- [Vue 3](https://vuejs.org/) — inline components in markdown
- [UnoCSS](https://unocss.dev/) — utility-first styling

## License

MIT
