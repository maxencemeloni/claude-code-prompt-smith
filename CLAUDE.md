# Prompt Smith Development Context

This file provides context for AI assistants (Claude Code) when working on Prompt Smith itself.
It is NOT loaded when users run Prompt Smith commands in their own projects.

---

## Project Identity

Prompt Smith is a slash command for Claude Code that optimizes rough prompts into cleaner, more executable versions. The core principle is **fidelity first** — the optimized prompt must preserve the user's exact intent while improving clarity, structure, and actionability.

---

## Understanding Suggestions

When the user proposes an idea or improvement, **always clarify the intent first** before responding:

- **"For the users"** — The suggestion is about what Prompt Smith should **do for people who run the command**. This means improving the optimization logic, adding modes, or changing how the preview/confirmation works.
- **"For the tool"** — The suggestion is about improving Prompt Smith's **internal structure**, commands, or architecture. This is contributor/maintainer work.

**Do not assume.** If the intent is ambiguous, ask: *"Is this something Prompt Smith should do when optimizing prompts, or a change to how Prompt Smith itself works?"*

---

## Design Principles

1. **Fidelity first** — Never silently change the user's intended outcome
2. **Claude Code native** — Optimized prompts should be terminal-ready instructions, not generic chat
3. **Minimal structure** — Add structure only when it improves execution quality
4. **Confirmation by default** — Never execute without explicit user consent (unless `--yes`)
5. **Developer respect** — No dumbed-down language; users are professionals

---

## Optimization Modes

| Mode | Purpose | When to Use |
|------|---------|-------------|
| `default` | General cleanup | Most prompts |
| `agentic` | Execution-focused structure | Orchestration, automation, multi-step delivery |
| `compact` | Shortest clean version | Utility prompts, brevity wanted |
| `strict` | Maximum fidelity | Sensitive wording, policy text |

---

## What's Explicitly Out of Scope

| Out of Scope | Why |
|--------------|-----|
| Code analysis tool | It optimizes prompts, not code |
| Repo refactoring tool | It rewrites prompts, not files |
| Task-specific plugin | It's a prompt optimizer and launcher |
| Autonomous executor | It requires confirmation before action |

---

## Commands Overview

| Command | Purpose |
|---------|---------|
| `/prompt` | Optimize a rough prompt with mode selection, preview, and confirmation |
| `/release` | Automate the full version release flow (version bump, changelog, commit, push, GitHub Release) |

### `/prompt` Workflow

1. Parse flags and raw prompt from `$ARGUMENTS`
2. Select or infer optimization mode
3. Show preview (mode, rationale, original, optimized, what changed)
4. Wait for confirmation (execute / edit / regenerate / cancel)
5. Execute the optimized prompt if confirmed

### Supported Flags

| Flag | Purpose |
|------|---------|
| `--mode <mode>` | Select optimization mode |
| `--yes` | Skip confirmation and execute immediately |
| `--dry-run` | Show optimized prompt without executing |
| `--list-modes` | Show available modes |
| `--help` | Show usage information |

---

## Version Management

### Versioning Strategy

- **Patch (x.x.1)** — Wording improvements, documentation fixes, non-breaking prompt tuning
- **Minor (x.1.0)** — New flags, new modes, improved interaction patterns, non-breaking behavior changes
- **Major (2.0.0)** — Breaking command syntax, renamed modes, incompatible execution behavior, major UX changes

### Releasing

Use `/release <version> <description>` to automate the full release flow. It handles version bumps, changelog, commit, push, and GitHub Release creation.

### Files Updated During Release

| File | What to Update |
|------|----------------|
| `VERSION` | Replace contents with new version |
| `.claude-plugin/plugin.json` | Update `"version"` field |
| `.claude-plugin/marketplace.json` | Update `"version"` in plugins array |
| `README.md` | Version badge |
| `CHANGELOG.md` | Add new version section at top |

### Post-Release Verification

After pushing, verify the plugin update works:
```bash
claude plugin marketplace update prompt-smith-marketplace
claude plugin update prompt-smith@prompt-smith-marketplace
```

---

## Repository Structure

```
claude-code-prompt-smith/
├── .claude-plugin/
│   ├── marketplace.json    # Marketplace manifest (version + metadata)
│   └── plugin.json         # Plugin manifest
├── .claude/
│   ├── commands/           # Dev-time slash commands (local development)
│   │   ├── prompt.md
│   │   └── release.md
│   └── settings.json       # Project permissions (deny rules)
├── commands/               # Plugin commands (distributed to users)
│   └── prompt.md
├── assets/                 # Banner and logo images
├── CLAUDE.md               # This file (development context)
├── CHANGELOG.md            # Changelog
├── LICENSE                 # MIT license
├── PROMPT_SMITH.md         # Core identity document (loaded by commands)
├── README.md               # User-facing documentation
└── VERSION                 # Current version
```

---

## Local Testing

- **Dev command:** `.claude/commands/prompt.md` — runs in this repo only, reads `PROMPT_SMITH.md` from project root
- **Plugin command:** `commands/prompt.md` — distributed to users, reads from `${CLAUDE_PLUGIN_ROOT}`

After modifying either file, keep them in sync. The only difference should be the `PROMPT_SMITH.md` path and its error message.

To verify sync: `diff .claude/commands/prompt.md commands/prompt.md` — should show only the path line.

## Test Prompts

Use these to verify each mode works correctly before releasing:

| Prompt | Expected Mode | Notes |
|--------|---------------|-------|
| `fix the bug` | default | Simple cleanup |
| `orchestrate the deploy pipeline with validation at each step` | agentic | Multi-step execution |
| `rename x to y` | compact | Trivial change |
| `Update the privacy policy section 3.2 to reflect the new data retention period` | strict | Sensitive text |
| `--help` | N/A | Should show usage, not optimize |
| `--dry-run Refactor the auth module` | default | Should show preview only, no execute option |
| (empty) | N/A | Should show usage |

---

## Common Development Tasks

| Change | Files to Update | Version Bump |
|--------|----------------|--------------|
| New mode | `PROMPT_SMITH.md`, both command files, `README.md` | minor |
| Mode behavior change | `PROMPT_SMITH.md`, both command files | patch |
| New flag | Both command files, `PROMPT_SMITH.md`, `README.md` | minor |
| New command | Both command dirs, `README.md`, this file | minor |

---

## Links

- **Repository:** https://github.com/maxencemeloni/claude-code-prompt-smith
- **Website:** https://prompt-smith.mmapi.fr/
