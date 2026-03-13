## OX

OX is a Hugo-native, high-neon, mono-first theme for blog and docs-lite publishing.

### Module identity

- Module path: `github.com/dan-hill/ox`
- In this repo family, OX is intended to be consumed by `site-base`, which is then consumed by `www` and `docs`.

### Installation

1. Copy `themes/ox/` into your Hugo site's `themes/` directory.
2. Set `theme = 'ox'` in your site config.
3. Keep Hugo's current template system layout in your site overrides (`layouts/baseof.html`, `layouts/page.html`, `layouts/section.html`, `layouts/_partials/`, `layouts/_shortcodes/`).

### Config basics

- Set `title` and `params.description`
- Optional hero settings live under `[params.ox.hero]`
- Main navigation can be configured with `[[menu.main]]`
- Taxonomies work out of the box with standard Hugo `tags` and `categories`

### Supported templates and sections

- home page with hero and featured content
- list and section pages with card grids and pagination
- single/page templates with metadata and optional TOC
- taxonomy and term pages
- docs-lite section patterns for `/docs/` content trees
- shortcodes: `panel`, `badge`, `callout`, `glow-button`

### Example site

Run the example site from `exampleSite/` with:

- `cd exampleSite && hugo server --themesDir ../themes`

Build it with:

- `cd exampleSite && hugo --themesDir ../themes`

### Repo-chain usage

For the current multi-repo setup:

- `github.com/dan-hill/ox` provides the shared presentation layer
- `github.com/dan-hill/site-base` imports OX as a Hugo module
- `github.com/dan-hill/www` and `github.com/dan-hill/docs` import `site-base`

That keeps OX reusable while allowing site-specific overrides in downstream repos.

### Asset attribution model

OX does **not** directly import Cyberpunk-Neon CSS, images, icons, or third-party brand assets.
The visual language is recreated from the approved OpenClaw reference-only inventory.
See `themes/ox/data/ox/attribution.yaml` for the reference ledger.

The repo also ships a precompiled `themes/ox/static/ox.css` so the example site builds on non-extended Hugo installations, while the SCSS source tree remains available under `themes/ox/assets/scss/`.

### GitHub Actions / deploy note

The downstream Pages workflows in `www` and `docs` can use standard Hugo because OX ships precompiled runtime CSS in `themes/ox/static/ox.css`.

Before downstream deploys can resolve OX remotely, OpenClaw should:

1. push and tag `github.com/dan-hill/ox`
2. in `site-base`, run `hugo mod get github.com/dan-hill/ox@<tag>`
3. commit the resulting `go.mod`/`go.sum` updates in `site-base`
4. tag and push `site-base`

### Font notes

OX uses an Iosevka-first mono stack. For the intended result, self-host minimal Iosevka WOFF2 files (regular, italic, semibold/bold) or install Iosevka locally. The theme falls back to other monospace fonts automatically.