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

## [ ] 1. Commit the local toolchain fix

Uncommitted on branch `track/leadership`:
- `.ruby-version` (new) → `3.3.11`
- `Gemfile.lock` (modified) → added `arm64-darwin` platform + native arm64 gem variants

**Why parked:** wanted to keep it out of the current content branch's scope.
**Action:** stage and commit these on the appropriate branch (likely `main` / a small
infra branch) so the arm64 platform + Ruby pin are shared and reproducible.

---

## [ ] 2. Modernize the GitHub Actions workflow

Current `.github/workflows/jekyll.yml` builds inside the `jekyll/builder:latest`
Docker container.

**Problems:**
- `jekyll/builder` is a **deprecated, unmaintained** image; `latest` pins an old
  Jekyll that **mismatches this repo's Gemfile (Jekyll 4.3.4)**.
- The job only builds to `_site` — there is **no deploy step**, so it's just a build
  check, not what publishes the site.
- CI does not use the repo's actual Gemfile/Ruby, so local and CI can drift.

**Note:** This is independent of the local Ruby fix above — CI runs in a container and
was not affected by the local breakage.

**Proposed replacement:** the official GitHub Pages flow, which uses this repo's real
Gemfile (same Jekyll 4.3.4 as local) and actually deploys:
- `ruby/setup-ruby` (with `bundler-cache: true`, Ruby `3.3`)
- `bundle exec jekyll build`
- `actions/configure-pages` → `actions/upload-pages-artifact` → `actions/deploy-pages`

Also confirm the repo's **Pages source setting** (Settings → Pages): "GitHub Actions"
vs "Deploy from a branch" — the native branch build only supports Jekyll 3.x via the
`github-pages` gem and would conflict with the pinned Jekyll 4.3.4.

---

## Housekeeping (nice-to-have)

- [ ] Retire the orphaned Intel RVM Ruby (`~/.rvm/rubies/ruby-2.7.5`) and stale
      Ruby PATH leftovers in `~/.zshrc` (e.g. `/usr/local/lib/ruby/gems/3.0.0/bin`,
      `$HOME/.rvm/bin`) once nothing else depends on them.
- [ ] Address pre-existing Sass `/`-division deprecation warnings in
      `_sass/_responsive.scss` (migrate to `math.div(...)`) before Dart Sass 2.0.
