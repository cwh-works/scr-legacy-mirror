# Short Creek Realty — Transitional Landing Page

A single-page transitional website announcing that **Excel Realty Consultants is
becoming Short Creek Realty**. One shared codebase serves both domains with an
identical experience:

| Domain | Role |
| --- | --- |
| https://www.shortcreekrealty.com | Canonical domain |
| https://www.excelrealty.us | Transitional legacy domain (same page) |

Both apex domains (`shortcreekrealty.com`, `excelrealty.us`) redirect to their
`www` counterparts via GitHub Pages.

## How it is deployed

- **This repository (`charles403/shortcreek-realty-site`) is the single source
  of truth.** It is published with GitHub Pages (branch `main`, root) at
  `www.shortcreekrealty.com`.
- **`charles403/excelrealty-legacy-site` is an auto-generated mirror.** Never
  edit it directly. On every push to `main` here, the GitHub Action in
  [.github/workflows/sync-mirror.yml](.github/workflows/sync-mirror.yml)
  force-pushes an identical copy to the mirror (only the `CNAME` file differs,
  pointing at `www.excelrealty.us`). The mirror is published with GitHub Pages
  at `www.excelrealty.us`.
- The workflow needs a repository secret **`MIRROR_TOKEN`**: a GitHub token
  with push access to `excelrealty-legacy-site`. A fine-grained personal access
  token scoped to only that repository (Contents: read and write) is
  recommended.

So: **edit files here, push to `main`, and both domains update.**

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole page, including the inline SVG backdrop |
| `assets/styles.css` | All styling and the animation system |
| `assets/og-image.png` | Social sharing image (1200×630) |
| `favicon.svg` | "SC" monogram favicon |
| `404.html` | Not-found page |
| `CNAME` | Custom domain for GitHub Pages (differs in the mirror) |
| `docs/BACKDROP.md` | Backdrop asset documentation and replacement guide |
| `docs/DNS.md` | DNS configuration: what was changed, what must be preserved |
| `CHANGELOG.md` | Everything created or changed during this project |

## How to update the wording

Edit the copy inside `<main class="hero">` in `index.html`, commit, and push to
`main`. The mirror syncs automatically. Also update `<title>`,
`meta description`, and the Open Graph tags if the message changes materially.

## The backdrop and animation

The backdrop is an **original AI-generated vector illustration** (layered SVG
inline in `index.html`) of a high-desert valley at dusk — mesas, canyon walls,
a creek catching the last light, sage on the valley floor. It is artwork
inspired by the Short Creek region, **not a photograph of any real place or
property**. See [docs/BACKDROP.md](docs/BACKDROP.md) for full provenance and
how to replace it later (e.g., with a licensed photo or video).

Motion is deliberately restrained and defined entirely in
`assets/styles.css` inside a `@media (prefers-reduced-motion: no-preference)`
block:

- a very slow scene zoom (75 s alternating),
- gentle horizontal parallax on the far/mid/near landscape layers,
- slow cloud drift and a breathing sunset glow,
- a one-time fade-up of the text on load.

Users with **reduced motion** enabled get a completely static page — same
composition, no animation. There is no video, so there is no autoplay,
poster, or mobile-data concern; the page weighs only a few tens of KB plus
one web font and works well on slow rural connections.

## Accessibility and SEO

- Semantic HTML, one `h1`, logical heading structure, keyboard accessible
  (no interactive traps; the page has no forms and no fake CTAs).
- Text contrast is maintained by a fixed gradient scrim over the backdrop.
- Canonical URL on both domains: `https://www.shortcreekrealty.com/` — the
  legacy domain deliberately canonicalizes to the new brand.
- `robots.txt` allows crawling; no analytics, no cookies, no tracking.

## DNS

See [docs/DNS.md](docs/DNS.md). Summary: only the web records (apex `A`
records and `www` CNAME) point at GitHub Pages. **MX, SPF/TXT, and all other
records are untouched — Google Workspace email on both domains is unaffected.**
