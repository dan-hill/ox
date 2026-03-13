+++
title = 'Token Map'
date = 2026-03-13T10:00:00Z
description = 'Semantic token overview for OX.'
summary = 'The palette is mapped to semantic CSS variables instead of being scattered through components.'
weight = 21
tags = ['reference', 'tokens']
+++

## Core semantic tokens

| Token | Purpose |
| --- | --- |
| `bg-canvas` | Full-page background |
| `bg-panel` | Primary panel surface |
| `accent-primary` | Interactive magenta accents |
| `border-strong` | Cyan border and outline anchor |

## Why semantic tokens matter

{{< panel title="Single source of truth" >}}
Component styles read semantic variables from `:root`, which keeps the theme opinionated without hard-coding raw values into every selector.
{{< /panel >}}