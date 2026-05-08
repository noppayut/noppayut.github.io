# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## About this site

Personal academic website for **Noppayut Sriwatanasakdi (Mew)**, NLP Engineer at Square Enix AI & Arts Alchemy. Built on the [al-folio](https://github.com/alshedivat/al-folio) Jekyll theme and hosted on GitHub Pages at `noppayut.github.io`.

## Development commands

**Local development (Docker — recommended):**
```bash
docker compose pull
docker compose up       # serves at http://localhost:8080 with live reload
# or with slimmer image:
docker compose -f docker-compose-slim.yml up
```

**Local development (without Docker):**
```bash
bundle install
bundle exec jekyll serve --lsi   # serves at http://localhost:4000
```

**Build only:**
```bash
bundle exec jekyll build --lsi
```

**Lint / format (Prettier):**
```bash
npx prettier --check .   # check formatting
npx prettier --write .   # auto-fix formatting
```

**Manual deploy to `gh-pages` branch:**
```bash
bin/deploy
```
Normally not needed — GitHub Actions auto-deploys on every push to `master`.

## Architecture

Content is authored in Markdown/YAML and compiled to static HTML by Jekyll.

### Key content files to edit

| What to change | File(s) |
|---|---|
| Bio, intro text, profile photo | [`_pages/about.md`](_pages/about.md) |
| News items (home page) | [`_news/`](_news/) — one `.md` per item |
| Publications | [`_bibliography/papers.bib`](_bibliography/papers.bib) — BibTeX; auto-rendered by jekyll-scholar |
| CV page | [`_pages/vitae.md`](_pages/vitae.md) + PDF in [`download/`](download/) |
| CV structured data | [`_data/cv.yml`](_data/cv.yml) (YAML fallback) or `assets/json/resume.json` (jsonresume standard) |
| Projects | [`_projects/`](_projects/) — one `.md` per project |
| Blog posts | [`_posts/`](_posts/) — filename must be `YYYY-MM-DD-title.md` |
| Site-wide settings, social links, scholar config | [`_config.yml`](_config.yml) |
| GitHub repos shown on /repositories/ | [`_data/repositories.yml`](_data/repositories.yml) |
| Co-author links in publications | [`_data/coauthors.yml`](_data/coauthors.yml) |

### Theme customization

- Colors/themes: [`_sass/_themes.scss`](_sass/_themes.scss) — change `--global-theme-color`
- Color variables: [`_sass/_variables.scss`](_sass/_variables.scss)
- Layouts: [`_layouts/`](_layouts/) (Liquid templates)
- Reusable partials: [`_includes/`](_includes/) (Liquid/HTML)

### Deployment flow

`master` branch → GitHub Actions (`.github/workflows/`) → builds Jekyll → pushes to `gh-pages` branch → served by GitHub Pages. **Never manually edit `gh-pages`.**

### Publications setup

Author self-identification (for underlining your name) is configured in `_config.yml` under `scholar.last_name` / `scholar.first_name`. Extra BibTeX fields supported: `pdf`, `arxiv`, `code`, `poster`, `slides`, `video`, `abstract`, `bibtex_show`, `selected` (set `selected=true` to appear on the home page).

### CV page vs. vitae page

There are two CV-related pages: `/cv/` (rendered from `_data/cv.yml` or `assets/json/resume.json`) and `/vitae/` ([`_pages/vitae.md`](_pages/vitae.md)) which currently links to the PDF download. The PDF CVs live in [`download/`](download/) and are named with date suffixes (e.g. `NoppayutS-CV-24Nov.pdf`).
