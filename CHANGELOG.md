# Change Log

## 2026-07-10 — Initial build and launch

### Files created (this repository)

- `index.html` — the transitional landing page, including the inline SVG
  backdrop (original AI-generated vector illustration; see `docs/BACKDROP.md`)
- `assets/styles.css` — shared styles and the restrained animation system
  (scene zoom, layer parallax, cloud drift, glow breathing, text fade-in; all
  disabled under `prefers-reduced-motion`)
- `assets/og-image.png` — 1200×630 social-share image (headless-Chrome render
  of the page)
- `favicon.svg` — "SC" monogram favicon
- `404.html` — not-found page linking back to the home page
- `robots.txt` — allows crawling
- `CNAME` — `www.shortcreekrealty.com` (the mirror's copy says
  `www.excelrealty.us`)
- `.nojekyll` — disables Jekyll processing on GitHub Pages
- `.github/workflows/sync-mirror.yml` — auto-syncs every push to the mirror
  repository
- `README.md`, `docs/BACKDROP.md`, `docs/DNS.md`, `CHANGELOG.md`

### GitHub (deployment)

- Created repository `charles403/shortcreek-realty-site` (source of truth)
- Created repository `charles403/excelrealty-legacy-site` (auto-generated
  mirror — never edit directly)
- Enabled GitHub Pages on both repos (branch `main`, root)
- Set custom domains: `www.shortcreekrealty.com` (primary repo),
  `www.excelrealty.us` (mirror repo)
- Added Actions secret `MIRROR_TOKEN` to the primary repo (token used by the
  sync workflow to push to the mirror; recommend replacing with a fine-grained
  PAT scoped to only the mirror repo)
- Enabled "Enforce HTTPS" on both Pages sites (after certificate issuance)

### GoDaddy DNS (see docs/DNS.md for full before/after)

- excelrealty.us: apex `A` "Parked" → four GitHub Pages A records;
  `CNAME www` → `charles403.github.io.`
- shortcreekrealty.com: apex `A` "WebsiteBuilder Site" → four GitHub Pages A
  records; `CNAME www` → `charles403.github.io.`
- No MX, TXT (SPF/DKIM/DMARC/site-verification), NS, SOA, or
  `_domainconnect` records were touched on either domain — Google Workspace
  email unaffected.

### Hosting settings changed elsewhere

- None. The old GoDaddy Website Builder site for shortcreekrealty.com remains
  in the GoDaddy account, just no longer connected to the domain. No other
  websites, repositories, domains, or services were modified.
