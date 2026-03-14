## OX

OX is the canonical shared Hugo theme source for the current multi-repo stack. `www` and `docs` are consumers of this shared theme via `site-base`.

### Module identity

- Module path: `github.com/dan-hill/ox`
- In this repo family, OX is intended to be consumed by `site-base`, which is then consumed by `www` and `docs`.

### Installation

1. Copy `themes/ox/` into your Hugo site's `themes/` directory.
2. Set `theme = 'ox'` in your site config.
3. Keep Hugo's current template system layout in your site overrides (`layouts/baseof.html`, `layouts/page.html`, `layouts/section.html`, `layouts/_partials/`, `layouts/_shortcodes/`).

### Purpose and visual direction

- typography-first
- dark asphalt / black background
- restrained neon accents
- monospace, Unifont-led
- no JavaScript required for v1
- no cards, thumbnails, or hero images

### Mode behavior

`params.ox.mode` is authoritative.

Supported values:

- `landing`
- `directory`

#### `landing`

Renders:

- top nav
- divider
- ASCII masthead
- tagline
- optional home intro/body
- `ROUTES`
- `FEATURED`
- footer line

#### `directory`

Renders:

- top nav
- divider
- ASCII masthead
- tagline
- home body/content as the main content area
- configured landing routes above the body when present
- footer line

Directory mode does **not** auto-render featured projects.

### Shared params and defaults

Canonical namespace:

- `params.ox.tagline`
- `params.ox.footer_line`
- `params.ox.masthead_ascii`
- `params.ox.masthead_ascii_compact`
- `params.ox.landing_routes`

Backward-compatible top-level aliases are also read:

- `params.tagline`
- `params.footer_line`
- `params.masthead_ascii`
- `params.masthead_ascii_compact`
- `params.landing_routes`

Resolution order:

1. `params.ox.*`
2. top-level alias
3. built-in default

Exact defaults:

- tagline: `SOFTWARE / SYSTEMS / TOOLS / LINKS`
- footer line: `PUBLISHED WITH HUGO // ORG -> OX-HUGO`
- full masthead:
  - `+------------------------------------------------------------------+`
  - `|  ASPHALT // INDEX                                                |`
  - `+------------------------------------------------------------------+`
- compact masthead:
  - `[ ASPHALT // INDEX ]`
- featured empty state:
  - `NO FEATURED PROJECTS INDEXED`

### Landing routes shape

Canonical config:

- `params.ox.landing_routes`

Shape:

- array of objects with:
  - `label`
  - `url`
  - optional `note`

In landing mode:

- if configured, routes render exactly as provided
- otherwise OX auto-generates routes from:
  - `/projects/` labeled `PROJECT INDEX`
  - `/index.xml` labeled `RSS` when available
  - up to 3 featured projects using project primary-destination precedence

### Shared page and list behavior

- regular pages and singles render with a shared shell: nav, divider, title, content, footer
- non-project lists/sections render dense text rows rather than card grids
- generic row grammar is:
  1. `YYYY-MM-DD TITLE` when a meaningful date exists, otherwise `TITLE`
  2. one-line summary with safe fallback
  3. `open`

### Project params

Canonical field:

- `project_kind`

Backward-compatible alias:

- `kind`

Other supported params:

- `status = live | wip | lab | arc`
- `featured = true | false`
- `external_url`
- `source_url`
- `notes_url`
- `stack`
- `ascii`
- `year`
- optional `weight`

Project rules:

- kind resolution:
  1. `project_kind`
  2. legacy `kind`
- year:
  1. `params.year`
  2. `.Date.Year`
  3. `----`
- summary:
  1. explicit summary
  2. description
  3. safe derived one-line summary
  4. `NO SUMMARY`
- primary destination:
  1. `external_url`
  2. internal permalink
- extra links:
  - `source`
  - `notes`
- sorting:
  1. `weight` ascending when present
  2. date descending
  3. title ascending

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

For the approved `v0.5.0` release payload, `themes/ox/static/ox.css` is the canonical runtime artifact.

The old SCSS tree under `themes/ox/assets/scss/` is not the source of truth for this release, and SCSS parity is intentionally out of scope for this pass.

The repo still ships the precompiled `themes/ox/static/ox.css` so the example site and consumers build on non-extended Hugo installations.

### GitHub Actions / deploy note

The downstream Pages workflows in `www` and `docs` can use standard Hugo because OX ships precompiled runtime CSS in `themes/ox/static/ox.css`.

Before downstream deploys can resolve OX remotely, OpenClaw should:

1. push and tag `github.com/dan-hill/ox`
2. in `site-base`, run `hugo mod get github.com/dan-hill/ox@<tag>`
3. commit the resulting `go.mod`/`go.sum` updates in `site-base`
4. tag and push `site-base`

### Unifont asset / licensing handling

For v1, OX vendors the approved raw OTF directly:

- font: `themes/ox/static/fonts/unifont/unifont.otf`
- copyright notice: `themes/ox/static/fonts/unifont/licenses/unifont-copyright.txt`
- GPL text: `themes/ox/static/fonts/unifont/licenses/GPL-2.0.txt`

No conversion or subsetting pipeline is added in this version.

### ox-hugo project authoring example

Example subtree for a project entry exported into `content/projects/`:

- subtree title becomes the project title
- set `EXPORT_HUGO_SECTION` to `projects`
- set `project_kind` as the canonical kind field

Example:

- `* Example Tool`
- `:PROPERTIES:`
- `:EXPORT_FILE_NAME: example-tool`
- `:EXPORT_HUGO_SECTION: projects`
- `:EXPORT_HUGO_CUSTOM_FRONT_MATTER+: :status "live"`
- `:EXPORT_HUGO_CUSTOM_FRONT_MATTER+: :project_kind "tool"`
- `:EXPORT_HUGO_CUSTOM_FRONT_MATTER+: :featured true`
- `:EXPORT_HUGO_CUSTOM_FRONT_MATTER+: :source_url "https://github.com/example/tool"`
- `:END:`
- `One-line summary of the project.`