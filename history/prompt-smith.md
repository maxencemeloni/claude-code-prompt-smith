# Prompt Smith History

## Current version
- `1.0.0`

## Versioning policy
Semantic versioning:
- patch -> documentation, wording, and non-breaking prompt tuning
- minor -> new flags, new modes, improved UX, non-breaking feature additions
- major -> breaking invocation changes or incompatible behavior updates

## Releases

### 1.0.0 - 2026-04-09
Initial plugin template release.

Included:
- plugin manifest in `.claude-plugin/plugin.json`
- project command in `commands/prompt-smith.md`
- maintainer reference in `PROMPT_SMITH.md`
- user-facing `README.md`
- visual asset banner in `assets/prompt-smith-banner.svg`
- changelog and history scaffolding

Behavior shipped in 1.0.0:
- mode-aware prompt optimization
- four modes: default, agentic, compact, strict
- confirmation-first execution flow
- `--yes` bypass for direct execution
- support for `--mode ...` and `--list-modes`
