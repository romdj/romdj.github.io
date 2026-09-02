# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based personal resume/portfolio site deployed to GitHub Pages at `romdj.github.io`. The site uses a single-page layout composed of modular HTML includes driven by a central YAML data file.

## Commands

```bash
# Install dependencies
bundle install

# Build the site
bundle exec jekyll build

# Serve locally with live reload
bundle exec jekyll serve
# Opens at http://localhost:4000
```

## Architecture

**Data-driven pages**: Content lives in YAML data files, not in the HTML includes. Two of them:
- `_data/data.yml` drives the resume pages: `/` (one-pager) and `/detail/` (full chronological)
- `_data/advisory.yml` drives `/advisory/` (the AI-native organization architecture offering)

Editing content means editing the relevant data file. Note that name, contact email, and Elia achievements appear in both files — they are intentionally duplicated, so a change to one may need mirroring in the other.

**Rendering flow**:
- `index.html` loads `site.data.data` and includes each section partial in order
- `advisory.html` loads `site.data.advisory` via `_includes/advisory_body.html`
- Each `_includes/*.html` partial renders one section
- `_layouts/default.html` wraps everything with the base HTML shell
- Styles are in `_sass/`, compiled from `_base.scss`, `_default.scss`, `_responsive.scss`, `_print.scss`, `_mixins.scss`

**Key files**:
- `_data/data.yml` — resume content (edit this to update the CV)
- `_data/advisory.yml` — advisory offering content
- `_config.yml` — site-level settings (`open: true/false` gates the whole site, `theme_color`, `lang`, and the `exclude:` list keeping working material out of the built site)
- `_includes/` — one HTML partial per section
- `assets/images/` — profile photo and tech/education logos
- `tmp/` — gitignored. Holds private working material (reviewer output, target profile, recruiter leads) that must not ship publicly.

**Visibility toggles**: Most contact/section items in `data.yml` have a `display: true/false` flag to show or hide them without deleting content.
