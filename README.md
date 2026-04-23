# boomtown-toolkit-web

Starter Hugo repo for rebuilding **boomtown-toolkit.org** as a static site.

This scaffold is designed around three facts from the donor pages:

1. The homepage is a custom layout with a workflow image and positioned link overlays.
2. The tool pages mostly share one repeatable structure.
3. The new site chrome should come from the current UQ site, but the toolkit content should stay separate from that shell.

## What is in this starter

- **Hugo** structure with a custom homepage and a reusable tool-page template
- **data-driven tool navigation** from `data/tools.yaml`
- reusable partials for:
  - header
  - footer
  - workflow tabs
  - homepage flowchart
  - sidebar blocks
  - related tools/resources
- **GitHub Pages** workflow for Hugo deployment
- **Decap CMS stub** for content editing later
- placeholder content for tool pages `tk1` to `tk8`

## What you still need to swap in

### 1. UQ header and footer
The partials in `layouts/partials/header.html` and `layouts/partials/footer.html` are clean placeholders.
They are intentionally simple so you can replace them with the 2026 UQ donor markup without dragging in the whole source site.

### 2. UQ CSS / design system assets
This starter uses only `static/css/toolkit.css`.
When you wire in the real UQ shell, add the required CSS and JS assets in `layouts/partials/head.html` or directly in `baseof.html`.
Keep toolkit-specific overrides in `static/css/toolkit.css`.

### 3. Flowchart artwork
Replace `static/images/flowchart-placeholder.svg` with the real toolkit workflow image.
The positioned overlay links are driven by classes from `data/tools.yaml`.

### 4. Real page copy
Replace the placeholder Markdown in `content/tools/*.md` and `content/pages/*.md`.

## Local development

Install Hugo extended, then run:

```bash
hugo server
```

Site will be available at:

```bash
http://localhost:1313/
```

## Repo structure

```text
content/
  _index.md
  tools/
  pages/
data/
  tools.yaml
layouts/
  _default/
  partials/
  tools/
static/
  css/
  images/
  admin/
.github/workflows/
config/_default/hugo.toml
```

## Content model

### Tool pages
Each tool page can use front matter like:

```yaml
---
title: "Tool #1: Choosing what to measure and why"
menu_title: "Tool 1"
intro: "Short intro shown near the title."
layout: "single"
sidebar:
  enabled: true
  blocks:
    - title: "Help"
      body: "Short sidebar copy."
    - title: "Explore"
      body: "Another block."
related_tools:
  - tk2
  - tk3
resources:
  - title: "Related resource"
    url: "https://example.com/resource"
external_tools:
  - title: "ABS Data"
    url: "https://www.abs.gov.au/"
---
```

## Decap CMS
A basic stub lives in `static/admin/`.
It is **not** fully wired for production auth.
Treat it as a placeholder until you choose the GitHub OAuth / Decap setup you want.

## Security note
Do not use client-side username/password checks to protect genuinely restricted content.
If you later need real route protection, put the protected path behind **Cloudflare Access** or another real gate.
