# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static single-page documentation site for **iDBL 동네당구리그** (a billiards league app). The site is deployed on Vercel.

## Structure

The entire site is a **single HTML file** (`index.html`) with no build step or dependencies:

- All CSS is inline within `<style>` tags in the `<head>`
- All JavaScript is inline within a `<script>` tag at the bottom of `<body>`
- Screenshot images are stored in `images/` (numbered `01_`–`09_` by section order)
- `vercel.json` configures cache headers: images are immutable (1-year cache), `index.html` is no-cache

## Deployment

Push to `main` → Vercel auto-deploys. No build command needed (static file).

## Architecture of index.html

The file is organized in order: CSS custom properties → component styles → responsive styles → HTML → inline JS.

**Layout:** Fixed sidebar (`#sidebar`, 264px) + scrollable `#content`. On mobile (< 768px), the sidebar collapses behind a `#topbar` hamburger button with an overlay.

**Content sections:** Each section is an `<article id="...">` element. Section IDs map directly to sidebar `<a href="#id">` nav links. Sections are grouped under `<hr class="section-divider" data-label="...">` headings.

**JavaScript features (all vanilla, no libraries):**
- Sidebar accordion: `.nav-group-title` click toggles `.collapsed` class
- Active nav highlight: `IntersectionObserver` on all `article[id]` elements
- Scroll progress bar: `#progress-bar` width set from `window.scrollY`
- Smooth scroll: custom offset logic for mobile topbar height
- Lightbox: `.lightbox-trigger` images open `#lightbox` overlay on click

**CSS variables** are defined in `:root` — brand colors use `--c-brand` (green `#10B981`) and all semantic colors are tokenized.

## Adding a New Section

1. Add an `<article id="new-section-id" class="doc-section">` block in `#content`
2. Add a corresponding `<a href="#new-section-id" class="nav-link">` in the appropriate `<ul class="nav-group-links">` in the sidebar
3. If adding a screenshot, name it `NN_description.png` and place in `images/`; use `<img class="lightbox-trigger">` with `data-caption`
