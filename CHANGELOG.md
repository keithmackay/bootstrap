# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

## [Unreleased]

- Add --version flag support, reporting installed version and a best-effort GitHub update check
- Add Changelog section to README linking CHANGELOG.md
- Move --help content to help.md for progressive disclosure
- Make bootstrap safe to re-run on an already-bootstrapped project
- Add CHANGELOG.md seeded from commit history
- Bundle a CHANGELOG.md seed in the template for future bootstrapped projects
- Genericize bootstrap template files, remove HabitPeeps/Flutter specifics
- Fix remaining Flutter-specific term and undocumented PHASES_SUMMARY table
- Remove old pre-skill bootstrap command, superseded by SKILL.md

## [1.1.0] - 2026-08-20

- Bundle a default template/ folder and fall back to it when no sibling template exists
- Always use the bundled template, drop project-relative fallback, add --help usage instructions

## [1.0.0] - 2026-08-19

- Initial commit: bootstrap skill, cross-platform ports, README, MIT license
- Initial commit

