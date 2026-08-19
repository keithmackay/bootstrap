Let's start a new project.

Begin by copying everything recursively from ../template to this project
folder, then update the project name in all project files in this folder
to the name of the current project.

Once the template is copied, ask me two questions:

1. "Would you like to create a remote GitHub repository for this project?"
   - Options: Yes / No
   - Default: Yes (if I just press enter or say nothing, treat as Yes)

2. If I answer yes, ask: "Should the repository be public or private?"
   - Options: Public / Private
   - Default: Private (if I just press enter or say nothing, treat as Private)

Store these preferences for later use.

Next, I have an idea I want to talk through with you. Ask me what we're
going to build. Once I describe the idea, create a README.md file at the
project root with:
- Project name as the title
- A "Description" section with the idea I described
- An "Installation" section (placeholder)
- A "Usage" section (placeholder)
- A "License" section (placeholder)

After creating the README.md, initialize git (if not already initialized).
If a git repo is being created (or was just initialized), ensure `.envrc` is
listed in `.gitignore` (append it if the file exists but doesn't already
include it; create the file with that entry if it doesn't exist).

Commit all files with the message "Initial project setup with README".

If I requested a remote GitHub repository:
- Create the remote repo using `gh repo create` with the project folder name
- Set visibility to public or private based on my earlier answer
- Push the initial commit to the remote

Once the repository setup is complete, let me know, then enter planning mode
to begin the design session.

Now I'd like you to help me turn my idea into a fully formed design and spec
(and eventually an implementation plan).

Ask me questions, one at a time, to help refine the idea. Ideally, the
questions would be multiple choice, but open-ended questions are OK, too.

Don't forget: only one question per message. Once you believe you understand
what we're doing, stop and describe the design to me, in sections of maybe
200-300 words at a time, asking after each section whether it looks right
so far.

Once that thinking session is complete, and before starting the build of the
current project, I need your help to write out a comprehensive implementation
plan. Assume that the engineer has zero context for our codebase and
questionable taste. document everything they need to know. which files to
touch for each task, code, testing, docs they might need to check. how to test
it.

Give them the whole plan as numbered phases broken into bite-sized, numbered
tasks. DRY. YAGNI. TDD. Frequent commits. Assume they are a skilled developer,
but know almost nothing about our toolset or problem domain.
Assume they don't know good test design very well.

Please write out this plan, in full detail, into docs/plans/

After writing the detailed implementation plan, create a PHASES_SUMMARY.md file
in docs/plans/ that provides a high-level overview of all phases. This summary
should include:
- Each phase number, title, and goal
- List of tasks per phase (brief descriptions)
- Key deliverables for each phase
- Technology stack overview
- Key principles (YAGNI, DRY, TDD)
- Success criteria
- Post-launch maintenance guidance

The PHASES_SUMMARY should match the detailed plan exactly but be more concise,
serving as a quick reference guide to the implementation roadmap.

At the end of the detailed implementation plan, include a "Next Steps" section
with ideas for future enhancements beyond the initial launch. Each enhancement
idea should be clearly flagged with either [Keith's idea] or [Claude's idea]
to indicate its source. These are optional improvements that could be tackled
after the core site is launched and stable.
