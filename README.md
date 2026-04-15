# nirs4all Landing Page

Official landing page for [nirs4all](https://github.com/GBeurier/nirs4all) and [nirs4all Studio](https://github.com/GBeurier/nirs4all-webapp).

A single-file, zero-dependency static page — no build step, no framework.

## Hosting on GitHub Pages (nirs4all.github.io)

To serve this page at `https://nirs4all.github.io`:

1. Create a GitHub **organization** named `nirs4all` (if not already exists)
2. Fork or push this repository into that organization as **`nirs4all.github.io`**
3. Go to the repo **Settings → Pages**
4. Under **Source**, select **GitHub Actions**
5. Push to `main` — the included workflow deploys automatically

The page will then be live at `https://nirs4all.github.io`.

## Local preview

Open `index.html` directly in any browser — no server needed.

## Structure

```
nirs4all-page/
├── index.html              # The entire landing page (HTML + CSS + JS)
├── assets/                 # Logos and screenshots
│   ├── nirs4all_logo.png
│   ├── nirs4all_logo_green.png
│   ├── nirs4all.svg
│   ├── nirs4all.ico
│   ├── logo-cirad-en.jpg
│   ├── results-page.png
│   ├── runs-page.png
│   ├── predictions-page.png
│   └── inspector-after-refresh.jpg
└── .github/
    └── workflows/
        └── deploy.yml      # GitHub Actions deployment
```

## Content

- **Hero**: Logo, tagline, install command, CTA buttons
- **Overview**: nirs4all library vs Studio comparison
- **Features**: 6 key capability cards
- **Screenshots**: Tabbed gallery of Studio UI
- **Quick Start**: Tabbed code blocks (install, basic usage, advanced pipelines)
- **Team**: Gregory Beurier, Denis Cornet, Lauriane Rouan
- **Institutions**: CIRAD + UMR AGAP Institut
- **Publications**: Research papers using nirs4all + BibTeX citation
- **Resources**: All links (GitHub, Docs, PyPI, institutions)

## Credits

Developed at [CIRAD](https://www.cirad.fr) / [UMR AGAP Institut](https://umr-agap.cirad.fr)
by Gregory Beurier, Denis Cornet, and Lauriane Rouan.
