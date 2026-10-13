# Quarto theme

A shared look for our Quarto websites, packaged as a [Quarto](https://quarto.org/) format extension. Install it in a website project, set one line in `_quarto.yml`, and the site gets the same header, colours, layout and repository block as every other site that uses it. Built and maintained by [Atlas Bear Labs](https://github.com/atlas-bear); MIT licensed, so anyone may use it.

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

Leave the script line out and the header shows no repository block. Everything else is optional. To change a default, put it under the same key; for example a landing page without a sidebar:

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

## Update

When the theme changes here, run this in each site and commit the result:

```bash
quarto update atlas-bear/quarto-theme
```

Releases are tagged. To pin a site to a release rather than the latest commit:

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

[AI-Enhanced OSINT](https://atlas-bear.github.io/osint-ai-guide/), [Maritime and Supply Chain OSINT Tools](https://atlas-bear.github.io/osint-tools/), [Recommended Reading](https://atlas-bear.github.io/recommended-reading/) and the [Atlas Bear Library](https://atlas-bear.github.io/).

## Licence

MIT. The Octicons drawn by the repository block are MIT licensed by GitHub; the Flatly and Darkly themes are MIT licensed by Bootswatch and ship with Quarto.
