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

## Instructions

Begin by copying everything recursively from the `template/` folder bundled with this skill (resolved relative to this skill file's own location, e.g. `template/` next to this `SKILL.md`) to this project folder. Do not look for or use any project-relative `template` folder — only the bundled one. Once copied, update the project name in all project files in this folder to the name of the current project.

Once the template is copied, ask me two questions:

1. "Would you like to create a remote GitHub repository for this project?"
   - Options: Yes / No
   - Default: Yes (if I just press enter or say nothing, treat as Yes)

2. If I answer yes, ask: "Should the repository be public or private?"
   - Options: Public / Private
   - Default: Private (if I just press enter or say nothing, treat as Private)

Store these preferences for later use.

Next, I have an idea I want to talk through with you. Ask me what we're going to build. Once I describe the idea, create a README.md file at the project root with:
- Project name as the title
- A "Description" section with the idea I described
- An "Installation" section (placeholder)
- A "Usage" section (placeholder)
- A "License" section (placeholder)

After creating the README.md, initialize git (if not already initialized). If a git repo is being created (or was just initialized), ensure `.envrc` is listed in `.gitignore` (append it if the file exists but doesn't already include it; create the file with that entry if it doesn't exist).

Commit all files with the message "Initial project setup with README".

If I requested a remote GitHub repository:
- Create the remote repo using `gh repo create` with the project folder name
- Set visibility to public or private based on my earlier answer
- Push the initial commit to the remote

Once the repository setup is complete, let me know, then enter planning mode to begin the design session.

## Design Session

Ask me questions, one at a time, to help refine the idea. Ideally, the questions would be multiple choice, but open-ended questions are OK, too.

Only one question per message. Once you believe you understand what we're doing, stop and describe the design to me, in sections of maybe 200–300 words at a time, asking after each section whether it looks right so far.

## Implementation Plan

Once the design session is complete, write a comprehensive implementation plan. Assume the engineer has zero context for the codebase and questionable taste — document everything they need to know: which files to touch for each task, code, testing, docs to check, how to test it.

Give them the whole plan as numbered phases broken into bite-sized, numbered tasks. DRY. YAGNI. TDD. Frequent commits. Assume they are a skilled developer but know almost nothing about the toolset or problem domain. Assume they don't know good test design very well.

Write the full detailed plan into `docs/plans/`.

After writing the detailed plan, create a `PHASES_SUMMARY.md` file in `docs/plans/` with:
- Each phase number, title, and goal
- List of tasks per phase (brief descriptions)
- Key deliverables for each phase
- Technology stack overview
- Key principles (YAGNI, DRY, TDD)
- Success criteria
- Post-launch maintenance guidance

The PHASES_SUMMARY should match the detailed plan exactly but be more concise, serving as a quick reference guide.

At the end of the detailed plan, include a "Next Steps" section with ideas for future enhancements beyond the initial launch. Each enhancement idea should be clearly flagged with either [Keith's idea] or [Claude's idea] to indicate its source.
