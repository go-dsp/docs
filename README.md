# docs

[![docs](https://github.com/go-dsp/docs/actions/workflows/docs.yml/badge.svg)](https://github.com/go-dsp/docs/actions/workflows/docs.yml)
[![License](https://img.shields.io/badge/license-BSD--3--Clause-B3245F?style=flat-square)](LICENSE)

**The go-dsp documentation site**, published at
<https://go-dsp.github.io/docs/>.

A [Hugo](https://gohugo.io/) site with the [tannevaled/hextra](https://github.com/tannevaled/hextra)
fork of the [Hextra](https://github.com/imfing/hextra) theme, built the same way
as the [go-numerics documentation](https://github.com/go-numerics/docs), with
go-dsp's branding. It documents
[`go-dsp/signal`](https://github.com/go-dsp/signal), one section.

## Versions

`params.libraries` in `hugo.yaml` names the release of each library the pages
describe. A version of the documentation is **the newest minor version among
them**, or `main` while none is tagged:

| Source | Published under |
| --- | --- |
| branch `main`, with `params.libraries` in `hugo.yaml` | `https://go-dsp.github.io/docs/<MAJOR.MINOR>/`, or `/docs/main/` |
| the newest version (else `main`) | also `https://go-dsp.github.io/docs/latest/` |

`https://go-dsp.github.io/docs/` redirects to `latest/`. Each push to `main`
replaces the directory of the version it describes, and nothing else. The pages
describe **signal v0.1.0**, published under `0.1/`.

To document a new release, set its entry in `params.libraries` and update the
pages.

## Pages

A library's pages are its own documentation: its `README.md` becomes the
section's home and each `docs/*.md` a page, with the text unchanged and the
links pointed into this site. A comment at the top of each page names the
file and the release it came from. Change the text in the library first, then
here.

## Layout

| Path | What |
| --- | --- |
| `content/en/` | the pages; `_index.md` is the home, one directory per library, `weight` orders the sidebar |
| `i18n/en.yaml` | the site's strings, beside the theme's |
| `hugo.yaml` | `baseURL`, the library versions described, the navbar (version › theme › search › GitHub), the brand mounts |
| `layouts/_partials/custom/content-begin.html` | the outdated-version banner (reads `versions.json`) |
| `layouts/_partials/favicons.html` | the brand's favicons |
| `assets/css/custom.css` | the brand rose as Hextra's primary colour, the table headers |
| `themes/hextra` | submodule: [tannevaled/hextra](https://github.com/tannevaled/hextra), pinned to v0.16.0 |
| `branding` | submodule: [go-dsp/brand](https://github.com/go-dsp/brand) (the mark, its PNGs and ICO) |
| `scripts/publish-version.sh` | puts one build into a `gh-pages` checkout and rewrites `versions.json`, `latest` and the root redirect |

## Working locally

```sh
git clone --recurse-submodules https://github.com/go-dsp/docs.git
cd docs
mkdir -p data && go run github.com/tannevaled/hextra/cmd/pagehistory@v0.21.0 > data/pagehistory.json
hugo server --baseURL http://localhost:1313/docs/0.1/
```

then open <http://localhost:1313/docs/0.1/>. Hugo 0.146 or later; no Python,
no Node.

## Publication

`.github/workflows/docs.yml`:

| Job | When | What |
| --- | --- | --- |
| `build` | pull requests, `main` | builds with `--baseURL …/docs/<version>/`, checks internal links and anchors (lychee, offline), uploads the site |
| `links` | pull requests, `main` | fetches every external URL the pages name |
| `deploy` | `main` | `scripts/publish-version.sh` into `gh-pages` (started empty on the first deploy), then a commit and a push |

GitHub Pages serves the `gh-pages` branch.

## Licence

BSD-3-Clause.
