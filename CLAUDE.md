# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static personal website for Andrew Blooman (Cloud Security Engineer). No build system, no framework, no package manager — just HTML, CSS, and vanilla JS served directly from the filesystem or a simple HTTP server.

## Development

To preview locally, open any `.html` file in a browser directly, or serve with any static file server:

```bash
python3.14 -m http.server 8080
# then open http://localhost:8080
```

There are no build steps, linters, or tests.

## File structure

| File | Purpose |
|------|---------|
| `assets/style.css` | All styles — single file, section-commented |
| `assets/main.js` | All client JS — mobile nav, active link, scroll reveal, contact form |
| `assets/andrew.jpg` | Portrait photo |
| `index.html` | Home page |
| `about.html`, `career.html`, `skills.html`, `certifications.html`, `writing.html`, `contact.html` | Inner pages |

## Architecture

**Shared structure**: Every page repeats the same `<header>` and `<footer>` HTML — there is no templating engine. When updating nav links or footer content, edit every `.html` file.

**Design tokens**: All colours, fonts, spacing, and breakpoints are CSS custom properties defined in `:root` at the top of `style.css`. Change values there rather than overriding inline.

**Typography stack**: three families loaded from Google Fonts — `Fraunces` (display headings, `.font-display`), `Inter Tight` (body, `.font-body`), `JetBrains Mono` (labels/meta, `.font-mono`).

**Scroll reveal**: Elements with class `reveal` start invisible (`opacity:0; transform:translateY(18px)`) and gain class `in` when they enter the viewport via `IntersectionObserver` in `main.js`. Respects `prefers-reduced-motion`.

**Active nav**: `main.js` compares `window.location.pathname` against each `<a href>` to add class `active`. The active link gets an underline via `::after` on desktop; hidden on mobile.

**Contact form**: The form submits via `mailto:` (no backend). `main.js` intercepts submit and builds a `mailto:` URL from the form fields.

**Responsive breakpoints**: `820px` (hero/footer reflow to single column, mobile nav activates) and `720px` (timeline and section headings reflow).
