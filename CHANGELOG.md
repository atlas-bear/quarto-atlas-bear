# Changelog

All notable changes to the theme are recorded here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and versions follow [Semantic Versioning](https://semver.org/): a major version for a change that alters a site's look or requires a configuration change, a minor version for additions that leave existing sites as they are, a patch for fixes. Every release bumps `version` in `_extensions/atlas-bear/theme/_extension.yml` and is tagged, so a site can pin it with `quarto add atlas-bear/quarto-theme@v1.0.0`.

## [Unreleased]

## [1.2.0] - 2026-10-14

### Changed

- The navigation bar follows the usual order: site name on the left, the site's own links next to it, and the utilities (search, repository block, colour toggle) together at the right end. The repository block now sits with the utilities, shows the repository name without the owner (the owner is in the tooltip), is narrower, and is hidden where the menu collapses. The search box keeps one width when focused instead of growing and pushing the links aside, and links and the site name never wrap or truncate.

## [1.1.0] - 2026-10-14

### Added

- A Library search box for the navigation bar (`library-search.js`): one index of every site, fetched from the Library page and searched in the browser with MiniSearch, results grouped by site with the current site first, keyboard shortcuts, and light and dark styles. A site opts in with one script tag and `search: false`; see the README.

### Changed

- The README and the example say the shared theme and the Library rather than Atlas|Bear; the licence names AB//LABS (formerly Atlas|Bear Labs), which began as Atlas|Bear Labs and spun off from Atlas|Bear. Text only, no behaviour change.

## [1.0.0] - 2026-10-13

### Added

- The `atlas-bear/theme-html` format: light and dark themes on Flatly and Darkly with a blue grey header and indigo accents, a centred 1220px layout with configurable grid, table of contents and link defaults, and card styles for landing pages.
- `repo-stats.js`, shipped as a format resource: a repository block in the navigation bar showing the latest release, stars and forks with Octicons, read from the public GitHub API once a day per browser.
- An example site, a README and this changelog.
