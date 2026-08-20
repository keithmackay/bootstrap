bootstrap — start a new software project from scratch

WHAT IT DOES
  Copies a bundled template into a new project directory, sets up a
  README, initializes git, optionally creates a GitHub remote, then
  runs a guided design session (one question at a time) and writes a
  full phased implementation plan to docs/plans/.

WHAT IT NEEDS
  - Run from inside an empty (or new) project directory
  - `gh` CLI installed and authenticated, if creating a GitHub remote

HOW TO CUSTOMIZE THE TEMPLATE
  The files copied into every new project live in the template/ folder
  bundled alongside this skill (i.e. template/ next to this SKILL.md —
  find it by locating where this skill is installed, e.g.
  ~/.claude/skills/bootstrap/template/ in Claude Code). To change what
  gets copied into future projects, edit, add, or remove files directly
  inside that template/ folder. There is no per-project template
  override — every project bootstrapped with this skill pulls from that
  one shared location.

USAGE
  /bootstrap          Run the full bootstrap flow
  /bootstrap --help   Show this message and exit

FLAGS
  --help    Show this help message without making any changes
