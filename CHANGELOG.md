# Changelog

All notable changes to this template are recorded here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and adheres to
[Semantic Versioning](https://semver.org/).

## [Unreleased]

### Added
- Open-source setup: MIT `LICENSE`, `CONTRIBUTING.md`, issue / PR templates
- `examples/sample-comment-service/`: a fully filled-in reference sample (comment-generation service)
- README first screen: when-to-use / when-not-to-use, badges, clearer tagline
- Full bilingual (English / Chinese) docs: every core document now ships as `*.md` (English, primary) + `*.zh-CN.md` (Chinese), with a language switcher bar at the top

### Changed
- README "reference implementation" section now points to `examples/`
- Primary language switched to English; original Chinese content preserved in `*.zh-CN.md`

### Fixed
- Renamed evals placeholder directories (`example-scenario-a/b`) to drop angle brackets from paths (Windows compatibility)
- Added `docs/prd/README.md` directory note (the directory was referenced by `CLAUDE.md` but previously missing)
- Rewrote all git history to a privacy noreply email (removed leaked local usernames / machine names)

### Removed

---

> Maintenance notes:
> - After completing each `TASKS.md` task, append an entry under `[Unreleased]` (`### Added/Changed/Fixed`)
> - On release, change `[Unreleased]` to `[X.Y.Z] - YYYY-MM-DD` and open a fresh `[Unreleased]`
