# Changelog

All notable changes to this plugin are documented here.

## 1.1.0 — UX improvements, new flags, and repo rename

*Released: April 2026*

### Changes

- Renamed repository from `claude-caude-prompt-smith` to `claude-code-prompt-smith`
- Added `--help` flag with full usage block and examples
- Added `--dry-run` flag to preview optimized prompts without executing
- Added `edit` option after preview to refine the optimized prompt before executing
- Added "What changed" optimization delta summary in the preview output
- Added concrete usage template for empty input (matches `--help` output)
- Added `LICENSE` file (MIT)
- Added local testing docs and test prompts table to `CLAUDE.md`
- Added `/release` command reference in `CLAUDE.md`
- Condensed common development tasks into a single table in `CLAUDE.md`
- Updated `PROMPT_SMITH.md` with new flags and UX requirements
- Updated sample output in `README.md` to reflect new features
- Fixed changelog format consistency (em dash separator)
- Added `*.svg` to `.claudeignore`

---

## 1.0.0 — Initial release

*Released: April 2026*

### Changes

- Added `/prompt-smith` plugin command
- Added four optimization modes: default, agentic, compact, strict
- Added confirmation-first execution flow
- Added `--yes` to skip confirmation
- Added `PROMPT_SMITH.md` maintainer reference
- Added version history scaffold

---
