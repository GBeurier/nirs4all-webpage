# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

The public landing page for the nirs4all ecosystem, served at **[nirs4all.org](https://nirs4all.org)**. It is a single hand-written static page — no framework, no build step, no `package.json`, no dependencies to install. The entire site (HTML + CSS + JS) lives in **`index.html`** (~2400 lines). Everything else is assets and deploy/SEO plumbing.

This is one checkout in the larger nirs4all developer working tree; the ecosystem map and cross-project rules live in [`../CLAUDE.md`](../CLAUDE.md). This repo has no architectural coupling to the sibling projects — it only *links* to them.

## Preview & deploy

- **Local preview**: open `index.html` directly in a browser (`file://`). No server, no tooling. Some runtime features (dynamic version fetch, Google Fonts) hit the network but degrade gracefully offline.
- **Deploy**: `.github/workflows/deploy.yml` publishes to GitHub Pages on every push to `main` (or manual `workflow_dispatch`). It uploads the **entire repo root** as the Pages artifact — there is no build, so whatever is committed is what ships. The custom domain is pinned by `CNAME` (`nirs4all.org`); do not delete it.

## How `index.html` is organized

It's one file with three top-level regions. Use the section comment markers to navigate rather than scrolling blind:

- **`<head>` (lines ~1–227)** — heavy SEO surface: canonical/hreflang links, Open Graph + Twitter cards, and a `application/ld+json` **JSON-LD `@graph`** (Organization / SoftwareApplication / etc.). Keep these in sync with each other and with the actual content when titles, descriptions, or the logo change.
- **`<style>` (lines ~228–1119)** — all CSS, inline. Organized into labeled blocks with `/* ── Section Name ──── */` banners (Reset & Variables, Layout, Navigation, Hero, Overview, Features, … Footer, Animations, Responsive). The theme is driven by CSS custom properties defined in `:root`. Edit the relevant banner block; don't introduce a stylesheet file.
- **`<body>` (lines ~1120–2030)** — content as a stack of `<section id="…">` blocks: `hero`, `overview`, `screenshots`, `features`, `applications`, `ecosystem`, `install`, `team`, `institutions`, `publications`, `faq`, `links`.
- **`<script>` (lines ~2031–2387)** — all JS, inline, vanilla (no libraries).

### Section background system

Sections alternate backdrop treatments via a class on the `<section>`: `section-paper` (warm off-white with grid ruling), `section-dark` (deep navy, used for the Studio screenshot showcase), `section-aurora` (soft shifting colored blobs), `section-alt`. Reuse these rather than inventing new background styling so the alternation stays consistent.

### Runtime JS behaviors worth knowing

- **Live version fetching.** On load, the page fetches the latest library version from PyPI (`https://pypi.org/pypi/nirs4all/json`) and the latest Studio release from the GitHub API (`.../repos/GBeurier/nirs4all-studio/releases/latest`), then injects them into elements marked `data-lib-version` / `data-studio-version` (and `…-prefix` variants) and rewrites download/asset links. If you add a version badge or a download button, wire it through these `data-*` hooks instead of hardcoding a version.
- **Animated spectra** — a custom SVG animation (sine-wave "spectra" with dots and cross-spectral connector traces) rendered with `preserveAspectRatio="none"`, so dots are drawn as ellipses whose `rx/ry` counter the non-uniform scale. Touch with care.
- Screenshot **carousel** (auto-rotating, preloads/decodes images up front, pauses on hover and tab-hidden), **lightbox** (click image, Esc to close), **install tabs**, and **copy-to-clipboard** buttons (`.copy-btn`, `data-copy` or nearest `<pre>` text).

## Assets

Organized into subdirectories under `assets/`: `logos_ecosystem/`, `institutions/`, `screenshots_studio/`, `authors/`, `partners/`. When referencing an asset from `index.html`, use the full subdirectory path (e.g. `assets/screenshots_studio/results-page.png`). `.gitignore` excludes PowerPoint logo sources (`*.pptx`) and WSL `*:Zone.Identifier` metadata streams — those are not part of the deployed site.

## When you change content, keep the SEO files in sync

- **`sitemap.xml`** — bump `<lastmod>` and update `<image:image>` entries when you add/rename screenshots or pages. (Note: the `<image:loc>` paths currently point at `/assets/<file>` but the files now live under `assets/screenshots_studio/` after a reorg — fix these to the real paths if you touch the sitemap.)
- **`robots.txt`** — references the sitemap URL.
- **`<head>` meta + JSON-LD** in `index.html` — the title/description appear in several places (`<title>`, `description`, OG, Twitter, JSON-LD); change them together.

## Conventions

- Keep it a single self-contained `index.html` with zero build tooling and zero runtime dependencies beyond the CDN font and the two optional version APIs. Don't add a bundler, framework, or package manager.
- Vanilla JS only; match the existing inline `<script>` style.
