# Prompt Smith

Turn rough prompts into cleaner, more executable Claude Code prompts.

`Prompt Smith` is a Claude Code plugin command that:
- rewrites a rough prompt into a stronger version
- shows the optimized prompt in the terminal
- lets you change optimization mode
- asks for confirmation by default
- executes immediately only after confirmation or with `--yes`

## What it does

Prompt Smith is useful when you have a prompt that is:
- too messy
- too vague
- too verbose
- not structured enough for Claude Code
- good in intent but weak in execution quality

It optimizes the prompt without changing the goal.

## Modes

### `default`
General cleanup.

### `agentic`
Best for orchestration, execution, multi-step delivery, automation, repo work, and operational prompts.

### `compact`
Shortest clean version.

### `strict`
Minimal rewrite, maximum fidelity.

## Usage

### Fastest local test

From the parent directory of this plugin:

```bash
claude --plugin-dir ./prompt-smith
```

Then inside Claude Code:

```text
/prompt-smith Optimise ce prompt pour en faire une instruction Claude Code plus propre
```

If your Claude Code version requires namespacing for plugin commands, use:

```text
/prompt-smith:prompt-smith Optimise ce prompt pour en faire une instruction Claude Code plus propre
```

## Command syntax

```text
/prompt-smith [--mode default|agentic|compact|strict] [--yes] <prompt>
```

Examples:

```text
/prompt-smith Fais-moi un prompt plus clair pour refactorer cette feature
```

```text
/prompt-smith --mode agentic Tu vas organiser le travail en parallèle et valider chaque étape
```

```text
/prompt-smith --mode compact Réécris ce prompt pour qu'il soit plus net
```

```text
/prompt-smith --mode strict --yes Corrige ce prompt sans changer son intention
```

```text
/prompt-smith --list-modes
```

## Expected flow

1. You enter a rough prompt.
2. Prompt Smith selects or respects a mode.
3. It prints:
   - the selected mode
   - why it chose that mode
   - the original prompt
   - the optimized prompt
4. It asks what to do next.
5. You can:
   - execute
   - regenerate in another mode
   - cancel
6. If confirmed, it executes the optimized prompt immediately.

## Files

```text
prompt-smith/
├── .claude-plugin/
│   └── plugin.json
├── .claude/
│   └── history/
│       └── prompt-smith.md
├── assets/
│   └── prompt-smith-banner.svg
├── commands/
│   └── prompt-smith.md
├── CHANGELOG.md
├── PROMPT_SMITH.md
└── README.md
```

## Versioning

This plugin uses semantic versioning.

- patch -> wording and non-breaking tuning
- minor -> new flags, new modes, UX improvements
- major -> breaking changes in invocation or behavior

Current version: `1.0.0`

## Notes

- The plugin is designed to preserve intent first.
- Confirmation is required by default.
- `--yes` is the explicit bypass.
- `PROMPT_SMITH.md` is the maintainer reference for future edits.
