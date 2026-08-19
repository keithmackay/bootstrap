# bootstrap

Bootstraps a new software project from scratch: copies template files, sets up README, initializes git, optionally creates a GitHub repo, then guides through idea refinement, design, spec, and full implementation planning.

## Highlights

- **One command, full setup** — template copy, README, git init, and an optional GitHub remote (public or private) all happen before any design discussion starts
- **Guided design session** — asks one question at a time to refine a raw idea into a concrete spec, rather than demanding a fully-formed plan up front
- **Implementation-ready output** — produces a detailed, phased plan in `docs/plans/` plus a concise `PHASES_SUMMARY.md`, written for an engineer with zero context on the codebase
- **Idea provenance tracked** — every "Next Steps" enhancement idea in the generated plan is tagged `[Keith's idea]` or `[Claude's idea]`, so it's clear whose thinking drove which direction

## Usage

Invoke `/bootstrap` from a fresh project directory. It walks through:

1. Copies everything from `../template` into the current directory and updates the project name throughout
2. Asks whether to create a GitHub remote, and if so, public or private (defaults: yes / private)
3. Asks what you're building, then generates a starter `README.md` (Description, Installation, Usage, License placeholders)
4. Initializes git, ensures `.envrc` is gitignored, commits, and pushes to the remote if one was requested
5. Enters a design session — one question at a time — until the idea is well-defined
6. Writes a full phased implementation plan to `docs/plans/`, plus a `PHASES_SUMMARY.md` quick-reference

## Installation

### Claude Code

```bash
cp -r ~/.claude/skills/bootstrap/ ~/.claude/skills/bootstrap/
```

Already installed if this file is at `~/.claude/skills/bootstrap/`. Invoke with `/bootstrap`.

### Codex

Add an entry to your marketplace JSON (`~/.agents/plugins/marketplace.json`, create if absent):

```json
{
  "name": "personal",
  "interface": { "displayName": "Personal Plugins" },
  "plugins": [
    {
      "name": "bootstrap",
      "source": { "source": "local", "path": "/path/to/bootstrap/" },
      "policy": { "installation": "AVAILABLE", "authentication": "ON_INSTALL" },
      "category": "Productivity"
    }
  ]
}
```

### Antigravity

No special files needed — the root `SKILL.md` is natively compatible.

**Global install** (all workspaces):
```bash
cp -r /path/to/bootstrap/ ~/.gemini/antigravity/skills/bootstrap/
```

**Workspace install** (current project only):
```bash
cp -r /path/to/bootstrap/ .agents/skills/bootstrap/
```

### Gemini CLI

Gemini CLI installs extensions from GitHub:

```bash
gemini extensions install https://github.com/<owner>/bootstrap
```

The skill is auto-discovered from `GEMINI.md` after installation.

> **Note:** Gemini CLI requires the skill to be in a public GitHub repository. Local-only install is not directly supported.

## Compatibility

| Feature | Claude Code | Codex | Antigravity | Gemini CLI |
|---------|:-----------:|:-----:|:-----------:|:----------:|
| Core skill | ✅ | ✅ | ✅ | ✅ |
| `gh repo create` (requires `gh` CLI) | ✅ | ✅ | ✅ | ✅ |
| Planning mode (`EnterPlanMode`) | ✅ | ❌ | ❌ | ❌ |

Legend: ✅ Supported · ❌ Not supported

### Platform Limitations (Codex, Antigravity, Gemini CLI)

`EnterPlanMode` is a Claude Code-specific tool. On other platforms, the agent will proceed with the design session inline rather than entering a distinct planning mode.

## Contributing

This is a personal skill, but improvements are welcome — fork, branch, and open a pull request.

## License

[MIT](LICENSE)

## References

- **Claude Code Skills:** https://code.claude.com/docs/en/skills
- **Codex Plugins:** https://developers.openai.com/codex/plugins/build
- **Antigravity Skills:** https://antigravity.google/docs/skills
- **Gemini CLI Extensions:** https://github.com/google-gemini/gemini-cli/blob/main/docs/extension.md
- **Agent Skills open standard:** https://agentskills.io/home
