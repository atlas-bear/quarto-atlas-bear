# Quarto theme

A shared look for our Quarto websites, packaged as a [Quarto](https://quarto.org/) format extension: a blue grey header with indigo accents in light and dark modes, a centred page capped at 1220px, and a repository block in the navbar that shows the latest release, stars and forks.

It is used by [AI-Enhanced OSINT](https://github.com/atlas-bear/osint-ai-guide), [Maritime and Supply Chain OSINT Tools](https://github.com/atlas-bear/osint-tools), [Recommended Reading](https://github.com/atlas-bear/recommended-reading) and the [Atlas Bear Library](https://github.com/atlas-bear/atlas-bear.github.io).

## Use it

In the Quarto project directory (the one holding `_quarto.yml`):

```bash
quarto add atlas-bear/quarto-theme
```

That copies the extension into `_extensions/atlas-bear/theme/`, which you commit. Then set the format:

```yaml
format:
  atlas-bear/theme-html:
    include-after-body:
      text: '<script src="repo-stats.js" data-repo="atlas-bear/your-repo"></script>'
```

The `data-repo` attribute names the repository the navbar block describes. Anything under the format key (for example `toc-depth` or a different `grid`) overrides the extension's defaults.

## Update it

When the theme changes here, run `quarto update atlas-bear/quarto-theme` in each site and commit the result. Quarto vendors extensions into the project on purpose, so a site never changes until you update it.

## What is in it

| File | Purpose |
| --- | --- |
| `_extensions/atlas-bear/theme/_extension.yml` | Declares the `atlas-bear/theme-html` format: theme files, page grid, table of contents and link defaults, and the script as a format resource. |
| `theme.scss`, `theme-dark.scss` | Bootstrap variable overrides and rules on top of the Flatly and Darkly themes. |
| `repo-stats.js` | Draws the repository block from the public GitHub API, cached for a day in the browser. |

## Licence

MIT. The Octicons in the repository block are MIT licensed by GitHub.
