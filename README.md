## OX

OX is the canonical shared Hugo theme source for the current multi-repo stack. `www` and `docs` consume it through `site-base`.

### Module identity

- Module path: `github.com/dan-hill/ox`
- In this repo family, OX is intended to be consumed by `site-base`, which is then consumed by `www` and `docs`.

### Visual direction

OX is not meant to feel like a generic blog skin in monospace. The target is:

- BBS index energy
- cracktro / demoscene framing
- UNIX manpage density
- cyberdeck status-strip attitude
- typography-first delivery with no JS required

### Mode behavior

`params.ox.mode` is authoritative.

Supported values:

- `landing`
- `directory`

#### `landing`

Renders:

- top nav with status strip
- ASCII masthead
- route switchboard
- featured project block
- footer/status line

#### `directory`

Renders:

- top nav with status strip
- ASCII masthead
- optional route block
- body content as the main manual / directory surface
- footer/status line

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

Default tagline:

- `BBS / CRACKTRO / UNIX / CYBERDECK`

Default compact masthead:

- `[ ASPHALT//INDEX :: SIGNAL BOARD ]`

Default featured empty state:

- `NO FEATURED PROJECTS INDEXED`

### Shared row grammar

Generic list rows:

1. optional `[YYYY-MM-DD]`
2. uppercase title
3. summary prefixed like a prompt / operator note
4. `$ open ...`

Project rows:

1. `[STATUS] [KIND] YEAR TITLE`
2. summary line
3. `$ open ... // source ... // notes ...`

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
- sorting:
  1. `weight` ascending when present
  2. date descending
  3. title ascending

### Runtime artifact

For the current release line, `themes/ox/static/ox.css` is the canonical runtime artifact.

The old SCSS tree under `themes/ox/assets/scss/` is not the source of truth for this pass, and SCSS parity is intentionally out of scope.

### Unifont asset / licensing handling

For v1, OX vendors the approved raw OTF directly:

- font: `themes/ox/static/fonts/unifont/unifont.otf`
- copyright notice: `themes/ox/static/fonts/unifont/licenses/unifont-copyright.txt`
- GPL text: `themes/ox/static/fonts/unifont/licenses/GPL-2.0.txt`

### Repo-chain usage

- `github.com/dan-hill/ox` provides the shared presentation layer
- `github.com/dan-hill/site-base` imports OX as a Hugo module
- `github.com/dan-hill/www` and `github.com/dan-hill/docs` import `site-base`

### Example site

Run the example site from `exampleSite/` with:

- `cd exampleSite && hugo server --themesDir ../themes`

Build it with:

- `cd exampleSite && hugo --themesDir ../themes`
