---
name: bootstrap
description: Use when starting a new software project from scratch — copies template files, sets up README, initializes git, optionally creates a GitHub repo, then guides through idea refinement, design, spec, and full implementation planning.
---

# Bootstrap

## Overview

Bootstraps a new project end-to-end: template copy → README → git setup → GitHub repo (optional) → design session → implementation plan.

## Flags

### `--help`

If the user invokes this skill with a `--help` flag (e.g. `/bootstrap --help`), do not run the bootstrap flow. Instead, read and display the contents of `help.md` (in this skill's folder) verbatim, then stop — do not proceed to the Instructions section below.

### `--version`

If the user invokes this skill with a `--version` flag (e.g. `/bootstrap --version`), do not run the workflow. Instead:

1. Read the installed version from this skill's own manifest: `.claude-plugin/plugin.json` if present, else `.codex-plugin/plugin.json`, else `gemini-extension.json` — whichever exists for this platform install. If none exist (a bare Claude Code skill with only SKILL.md), read the topmost version heading in `CHANGELOG.md` instead.
2. Print: `bootstrap v<installed-version>`
3. Best-effort update check — determine this skill's GitHub source repo:
   a. If `.git` exists here and `git remote get-url origin` resolves to a `github.com` URL, use that `owner/repo`.
   b. Otherwise, search this skill's own `README.md` for the first `https://github.com/<owner>/<repo>` URL and use that.
   c. If neither yields a repo, or the `gh` CLI isn't installed/authenticated: stop here. Print nothing further — no status line, no error.
4. If a repo was found: run `gh api repos/<owner>/<repo>/releases/latest -q .tag_name` (strip a leading `v`). Compare to the installed version:
   - Equal → append: `Status: up to date`
   - Installed is older → append: `Status: newer version available (v<latest>). To update: if you installed this via a Claude Code marketplace, run /plugin marketplace update <marketplace-name> then reinstall; otherwise, git pull in your install directory if it's a git checkout, or re-copy from https://github.com/<owner>/<repo> per this README's Installation section.`
   - Installed is newer → append: `Status: ahead of latest release (development checkout)`
   - If the API call fails for any reason (network, auth, rate limit, malformed tag): print nothing further — no status line, no error shown to the user.
5. Stop — do not proceed to run the skill's actual workflow.

## Instructions

### Re-run safety check

Before doing anything else, check whether this project has already been bootstrapped (e.g. a `README.md`, a `.git` directory, or `docs/plans/` already exist in this folder). If it looks like bootstrap has already run here, stop and tell me what already exists, then ask whether I want to:
- Cancel, or
- Re-run anyway (in which case, treat every step below as idempotent per the notes inline — never blindly overwrite or duplicate existing work)

Do not silently overwrite existing files or redo already-completed setup steps.

Begin by copying everything recursively from the `template/` folder bundled with this skill (resolved relative to this skill file's own location, e.g. `template/` next to this `SKILL.md`) to this project folder. For any file that already exists at the destination, skip it (do not overwrite) and tell me which files were skipped — do not blindly clobber files I or a prior run may have already customized. Once copied, update the project name in all newly-copied project files in this folder to the name of the current project.

Once the template is copied, ask me two questions:

1. "Would you like to create a remote GitHub repository for this project?"
   - Options: Yes / No
   - Default: Yes (if I just press enter or say nothing, treat as Yes)

2. If I answer yes, ask: "Should the repository be public or private?"
   - Options: Public / Private
   - Default: Private (if I just press enter or say nothing, treat as Private)

Store these preferences for later use.

Next, I have an idea I want to talk through with you. Ask me what we're going to build. Once I describe the idea, create a README.md file at the project root — but only if one doesn't already exist. If `README.md` already exists, show me its current contents and ask whether to leave it as-is or replace it, rather than overwriting it automatically. A new README should have:
- Project name as the title
- A "Description" section with the idea I described
- An "Installation" section (placeholder)
- A "Usage" section (placeholder)
- A "License" section (placeholder)

After handling the README, initialize git only if `.git` doesn't already exist in this folder. Ensure `.envrc` is listed in `.gitignore` (append it if the file exists but doesn't already include it; create the file with that entry if it doesn't exist) — check first so the entry isn't duplicated on a re-run.

Check `git status` for staged/unstaged changes before committing. Only create a commit if there is something to commit — an empty repo with nothing changed since the last commit should not produce an empty commit. Use the message "Initial project setup with README" only for the very first commit in a fresh repo; if a commit history already exists, use a message describing what actually changed instead.

If I requested a remote GitHub repository:
- First check whether a remote named `origin` already exists (`git remote -v`). If it does, skip creation and tell me it's already configured rather than erroring out on `gh repo create`.
- Otherwise, create the remote repo using `gh repo create` with the project folder name, set visibility to public or private based on my earlier answer, and push the initial commit to the remote.

Once the repository setup is complete, let me know, then enter planning mode to begin the design session.

## Design Session

Ask me questions, one at a time, to help refine the idea. Ideally, the questions would be multiple choice, but open-ended questions are OK, too.

Only one question per message. Once you believe you understand what we're doing, stop and describe the design to me, in sections of maybe 200–300 words at a time, asking after each section whether it looks right so far.

## Implementation Plan

Once the design session is complete, write a comprehensive implementation plan. Assume the engineer has zero context for the codebase and questionable taste — document everything they need to know: which files to touch for each task, code, testing, docs to check, how to test it.

Give them the whole plan as numbered phases broken into bite-sized, numbered tasks. DRY. YAGNI. TDD. Frequent commits. Assume they are a skilled developer but know almost nothing about the toolset or problem domain. Assume they don't know good test design very well.

Write the full detailed plan into `docs/plans/`.

After writing the detailed plan, create a `PHASES_SUMMARY.md` file in `docs/plans/` with:
- A "Current Status" table listing every phase with a status marker (🔲 Not Started / 🟨 In Progress / ✅ Complete) — the bundled `/next` command reads this table to find the next phase to work on, so keep it up to date as phases progress
- Each phase number, title, and goal
- List of tasks per phase (brief descriptions)
- Key deliverables for each phase
- Technology stack overview
- Key principles (YAGNI, DRY, TDD)
- Success criteria
- Post-launch maintenance guidance

The PHASES_SUMMARY should match the detailed plan exactly but be more concise, serving as a quick reference guide.

At the end of the detailed plan, include a "Next Steps" section with ideas for future enhancements beyond the initial launch. Each enhancement idea should be clearly flagged with either [Keith's idea] or [Claude's idea] to indicate its source.
