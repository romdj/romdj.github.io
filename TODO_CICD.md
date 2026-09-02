# TODO — CI/CD & Local Toolchain

Parked follow-ups from the 2026-07-06 local environment fix (Ruby toolchain repair).
None of these block local development — `bundle exec jekyll serve` works today.

## Background

The local `jekyll serve` broke because the only project Ruby was an orphaned Intel
(x86_64) Ruby 2.7.5 under RVM, linked against Intel Homebrew's `libgmp.10.dylib`.
A Homebrew cleanup removed Intel Homebrew entirely (only `/opt/homebrew` ARM remains),
so that library disappeared and the Ruby binary could no longer start.

Fixed by moving to a native arm64 toolchain:
- Installed `rbenv` + `ruby-build` via Homebrew.
- Installed native **Ruby 3.3.11** (`rbenv global 3.3.11`); pinned via `.ruby-version`.
  (3.3 over 3.4 to avoid Jekyll 4.3 friction with stdlib gems dropped in Ruby 3.4.)
- Added `rbenv init` to `~/.zshrc` after the legacy RVM PATH so rbenv shims win.
- `bundle install` + `bundle lock --add-platform arm64-darwin` (lockfile was
  `x86_64-darwin-21` only).

---

## [x] 1. Commit the local toolchain fix

Done, on a later branch than originally parked here. The toolchain ended up moving
further than this note anticipated: instead of rbenv + Ruby 3.3.11, a second local
breakage (Homebrew `gmp` path gone after the Intel/Apple Silicon migration finally bit
the last `rvm` install) led to Homebrew Ruby 4.0.6 directly, no rbenv. `.ruby-version`
and `Gemfile.lock` are both committed and reflect that.

---

## [x] 2. Modernize the GitHub Actions workflow

Done. `.github/workflows/jekyll.yml` (the `jekyll/builder:latest` container build
described below) is deleted. `.github/workflows/deploy-pages.yml` is the sole
workflow now: `ruby/setup-ruby` reading `ruby-version: .ruby-version` (not a hardcoded
`"3.3"` — kept in sync with the local toolchain automatically), `bundle exec jekyll
build`, `configure-pages` → `upload-pages-artifact` → `deploy-pages`. Triggers on push
to `main` plus `workflow_dispatch`.

Confirmed as predicted: the old container workflow's problems were exactly as
diagnosed below, and it started hard-failing (`Bundler::GemNotFound`) the moment the
Ruby 4.0.6 lockfile regeneration landed, since the container's cached gems never
matched a Gemfile.lock they weren't built against.

**Still open, not yet confirmed:** the repo's Pages source setting (Settings → Pages
→ "GitHub Actions" vs "Deploy from a branch"). If it's still set to branch deploy,
this workflow builds and uploads an artifact that nothing consumes.

**Original diagnosis, kept for reference:**

Current `.github/workflows/jekyll.yml` builds inside the `jekyll/builder:latest`
Docker container.

**Problems:**
- `jekyll/builder` is a **deprecated, unmaintained** image; `latest` pins an old
  Jekyll that **mismatches this repo's Gemfile (Jekyll 4.3.4)**.
- The job only builds to `_site` — there is **no deploy step**, so it's just a build
  check, not what publishes the site.
- CI does not use the repo's actual Gemfile/Ruby, so local and CI can drift.

---

## Housekeeping (nice-to-have)

- [ ] Retire the orphaned Intel RVM Ruby (`~/.rvm/rubies/ruby-2.7.5`) and stale
      Ruby PATH leftovers in `~/.zshrc` (e.g. `/usr/local/lib/ruby/gems/3.0.0/bin`,
      `$HOME/.rvm/bin`) once nothing else depends on them.
- [ ] Address pre-existing Sass `/`-division deprecation warnings in
      `_sass/_responsive.scss` (migrate to `math.div(...)`) before Dart Sass 2.0.
