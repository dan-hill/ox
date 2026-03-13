+++
title = 'Getting Started'
date = 2026-03-13T09:15:00Z
description = 'Quick start guide for the OX theme.'
summary = 'Configure the theme, define menus, and publish docs pages with the same neon token system.'
featured = true
weight = 10
tags = ['guide', 'docs']
toc = true
+++

{{< badge tone="primary" >}}docs-lite{{< /badge >}}

## Install the theme

Copy `themes/ox` into your Hugo site and set `theme = 'ox'` in site config.

## Set the basics

{{< callout type="note" title="Start small" >}}
Set your site title, a short description, and a simple main menu. OX will take care of hero, cards, and typography without JavaScript.
{{< /callout >}}

### Enable docs content

Create content under `/docs/` and use headings naturally. The table of contents appears automatically when the page has nested headings.

## Example code block

```toml
[params.ox.hero]
title = 'Signal lock acquired'
primary_url = '/posts/'
secondary_url = '/docs/'
```