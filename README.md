# Quarto theme

A shared look for our Quarto websites, packaged as a [Quarto](https://quarto.org/) format extension. Install it in a website project, set one line in `_quarto.yml`, and the site gets the same header, colours, layout and repository block as every other site that uses it. Built and maintained by [AB//LABS](https://ab-labs.io); MIT licensed, so anyone may use it.

## What you get

- **Header and colours.** A blue grey navigation bar with indigo accents, softened body text, a tinted blockquote, and a matching dark mode behind Quarto's light and dark toggle. The light theme builds on Bootswatch Flatly, the dark one on Darkly.
- **Layout.** Page body and navigation bar capped at 1220px and centred, with a 270px sidebar, an 820px body and a 230px margin for the on-page table of contents. Each site may override the grid.
- **Repository block.** A small script draws the repository name, latest release, stars and forks in the navigation bar, with the same Octicons GitHub uses. It reads the public GitHub API once a day per browser, keeps the result in local storage, sets no cookies, and falls back to the name alone if the API is unreachable. Long repository names are shortened with an ellipsis.
- **Sensible defaults.** Table of contents on, external-link icons off, smooth scrolling on. Anything can be overridden per site.
- **Card grid.** Styles for a simple card grid (`.atlas-cards` and `.atlas-card`), used by listing templates on landing pages.

## Requirements

Quarto 1.10 or later. The extension has no other dependencies; the Bootswatch themes ship with Quarto.

## Install

In the Quarto project directory (the one holding `_quarto.yml`):

```bash
quarto add atlas-bear/quarto-theme
```

Quarto copies the extension into `_extensions/atlas-bear/theme/` in your project. Commit that directory: Quarto vendors extensions on purpose, so a site builds offline and never changes until you update it.

## Configure

Select the format and name the repository the header block should describe:

```yaml
format:
  atlas-bear/theme-html:
    include-after-body:
      text: '<script src="repo-stats.js" data-repo="your-org/your-repo"></script>'
```

The block sits at the right end of the bar with the search box and the colour toggle, shows the repository name with the owner in the tooltip, and is hidden where the menu collapses. Leave the script line out and the header shows no repository block. Everything else is optional. To change a default, put it under the same key; for example a landing page without a sidebar:

```yaml
format:
  atlas-bear/theme-html:
    include-after-body:
      text: '<script src="repo-stats.js" data-repo="your-org/your-repo"></script>'
    grid:
      sidebar-width: 0px
      body-width: 1000px
      margin-width: 0px
    toc: false
```

Site structure (navigation bar, sidebar, footer, search) is configured in each site's `_quarto.yml` as usual; the extension only sets the format.

## Library search

The theme can put a search box in the navigation bar that searches every site in the Library at once. One site, the Library page, publishes the index (`search-index.json`) and the search engine (`minisearch.min.js`, MIT); every other site loads both from there the first time a visitor types, so a site carries nothing but a script tag. Results are grouped by site with the current site first, and each opens the page, the section or the entry it names. The query never leaves the browser.

Turn Quarto's own search off and add the script after the repository block:

```yaml
website:
  search: false

format:
  atlas-bear/theme-html:
    include-after-body:
      text: '<script src="repo-stats.js" data-repo="your-org/your-repo"></script><script src="library-search.js" data-source="tools"></script>'
```

`data-source` is the site's key in the index, so its own results come first; `data-index` points at a different index if you run your own (the default is `https://library.ab-labs.io/search-index.json`). The index is built by `scripts/build_search.py` in the [atlas-bear.github.io](https://github.com/atlas-bear/atlas-bear.github.io) repository, which also explains how a site is added to it. In the browser, `/` or Ctrl+K (Cmd+K on a Mac) focuses the box, the arrow keys move through the results, Enter opens one and Esc closes the list.

## Update

When the theme changes here, run this in each site and commit the result:

```bash
quarto update atlas-bear/quarto-theme
```

Releases are tagged and listed in the [CHANGELOG](CHANGELOG.md). To pin a site to a release rather than the latest commit:

```bash
quarto add atlas-bear/quarto-theme@v1.0.0
```

## Customise

The colours and type are Bootstrap variables at the top of `theme.scss` and `theme-dark.scss`. A site that needs a different accent, or extra rules of its own, can add its own SCSS file after the extension's by listing the theme explicitly:

```yaml
format:
  atlas-bear/theme-html:
    theme:
      light: [flatly, _extensions/atlas-bear/theme/theme.scss, custom.scss]
      dark: [darkly, _extensions/atlas-bear/theme/theme-dark.scss, custom-dark.scss]
```

If a change would suit every site, change it here instead and open a pull request.

## What is in the repository

| Path | Purpose |
| --- | --- |
| `_extensions/atlas-bear/theme/_extension.yml` | Declares the `atlas-bear/theme-html` format: theme files, grid, defaults, and the script as a format resource. |
| `_extensions/atlas-bear/theme/theme.scss` | Light theme: Bootstrap variable overrides and rules on top of Flatly. |
| `_extensions/atlas-bear/theme/theme-dark.scss` | Dark theme: the same on top of Darkly. |
| `_extensions/atlas-bear/theme/repo-stats.js` | The repository block in the navigation bar. |
| `example/` | A minimal site that uses the theme. |

## Sites using it

[AI-Enhanced OSINT](https://library.ab-labs.io/osint-ai-guide/), [Maritime and Supply Chain OSINT Tools](https://library.ab-labs.io/osint-tools/), [Recommended Reading](https://library.ab-labs.io/recommended-reading/) and the [Library](https://library.ab-labs.io/).

## Licence

MIT. The Octicons drawn by the repository block are MIT licensed by GitHub; the Flatly and Darkly themes are MIT licensed by Bootswatch and ship with Quarto.
