# PROMPT_SMITH.md

## Purpose

Prompt Smith is a Claude Code plugin focused on one thing:
turning rough prompts into prompts that are clearer, tighter, more actionable, and more reliable to execute.

It is designed for users who already think in prompts and want a repeatable way to improve prompt quality without rewriting everything by hand.

## Product behavior

When the user runs `/prompt-smith <prompt>` the plugin should:
1. parse optional flags
2. identify the best optimization mode
3. display the original prompt
4. display the optimized prompt
5. ask for confirmation by default
6. execute only after confirmation
7. allow a direct bypass with `--yes`

## Supported flags

- `--mode default`
- `--mode agentic`
- `--mode compact`
- `--mode strict`
- `--yes`
- `--list-modes`

## Optimization philosophy

### 1. Fidelity first
The plugin must preserve the user's real intent.
It can improve structure, wording, and precision, but it must not silently widen the scope.

### 2. Claude Code native output
The optimized prompt should read like something meant to drive Claude Code in a terminal workflow, not like a generic chat prompt.

### 3. Use structure only when it helps
Not every prompt should become a large framework.
The structure should fit the task.

### 4. Confirm before action
Unless `--yes` is present, Prompt Smith should not execute the optimized prompt immediately.
The user must review and confirm first.

## Mode definitions

### default
General cleanup mode.
Best for most prompts.

### agentic
Execution-heavy mode.
Best for orchestration, delivery, repo work, automation, planning, and multi-agent prompts.

Recommended structure when it helps:
- role
- objective
- constraints
- workflow
- validations
- deliverables
- priorities

### compact
Shortest useful rewrite.
Best when the user wants speed and low verbosity.

### strict
Minimal rewrite mode.
Best when the wording is sensitive and must stay very close to the source.

## UX requirements

The preview should always be terminal-friendly and easy to scan.
Preferred order:
- title
- selected mode
- why this mode
- available modes
- original prompt
- optimized prompt
- next actions

## Confirmation contract

Default actions after preview:
- `execute`
- `regenerate default`
- `regenerate agentic`
- `regenerate compact`
- `regenerate strict`
- `cancel`

If confirmed, the plugin should execute the optimized prompt in the same interaction.

## Versioning rules

Use semantic versioning.

- patch: wording improvements, documentation fixes, non-breaking prompt tuning
- minor: new flags, new modes, improved interaction patterns, non-breaking behavior changes
- major: breaking command syntax, renamed modes, incompatible execution behavior, major UX changes

## Non-goals

Prompt Smith is not:
- a general code analysis plugin
- an autonomous repo refactoring tool by itself
- a replacement for task-specific plugins

It is a prompt optimizer and launcher.
