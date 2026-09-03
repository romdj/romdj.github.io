# romdj.github.io

Personal site: résumé and an advisory offering, built with Jekyll and deployed to
GitHub Pages.

**Live:** [romdj.github.io](https://romdj.github.io)

## Site structure

```
/              market selector
/be/           Belgian résumé, one-pager
/be/detail/    Belgian résumé, full chronological
/ch/           Swiss résumé, one-pager
/ch/detail/    Swiss résumé, full chronological
/advisory/     AI-native organization architecture, advisory offering
```

The two market résumés share one data source (`_data/data.yml`). Contact details,
languages, sports ordering, and a couple of experience entries differ by market;
everything else — profile, impact, capabilities, employment history — is identical.
A page opts into the Swiss variant by setting `variant: ch` in its front matter; the
includes fall back to the default (Belgian) values when no override is present. See
`CLAUDE.md` for how that mechanism works.

`/advisory/` is a separate pitch, not a résumé variant, and has its own data file
(`_data/advisory.yml`).

## Running locally

Requires the Ruby version pinned in `.ruby-version` (currently 4.0.6). Any Ruby
version manager works — the commands below assume Homebrew's `ruby` formula, which
is what this repo is developed against.

```bash
git clone https://github.com/romdj/romdj.github.io.git
cd romdj.github.io
bundle install
bundle exec jekyll serve
```

Open `http://localhost:4000`.

If `bundle install` or `jekyll serve` fails with gem or dependency errors, the most
likely cause is a Ruby version mismatch — confirm `ruby -v` matches `.ruby-version`
before troubleshooting anything else.

## Deployment

Deploys via GitHub Actions on every push to `main` (`.github/workflows/deploy-pages.yml`).
The same workflow runs on pull requests as a build-only check — it builds the site
and uploads the artifact, but the deploy step is skipped outside of `main`, so a PR
can never publish unmerged content.

Requires the repository's **Settings → Pages → Source** set to **GitHub Actions**.

## Acknowledgments

Built on Tarrex's [online-resume](https://github.com/tarrex/online-resume), whom I
thank for the clean, to-the-point template.
