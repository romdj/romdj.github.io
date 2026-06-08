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

**Single source of truth**: All resume content lives in `_data/data.yml`. This file drives every section of the page — editing content means editing this file, not the HTML includes.

**Rendering flow**:
- `index.html` loads `site.data.data` and includes each section partial in order
- Each `_includes/*.html` partial renders one resume section (experiences, skills, education, etc.)
- `_layouts/default.html` wraps everything with the base HTML shell
- Styles are in `_sass/`, compiled from `_base.scss`, `_default.scss`, `_responsive.scss`, `_print.scss`, `_mixins.scss`

**Key files**:
- `_data/data.yml` — all resume content (edit this to update the CV)
- `_config.yml` — site-level settings (`open: true/false` gates the whole site, `theme_color`, `lang`)
- `_includes/` — one HTML partial per resume section
- `assets/images/` — profile photo and tech/education logos

**Visibility toggles**: Most contact/section items in `data.yml` have a `display: true/false` flag to show or hide them without deleting content.
