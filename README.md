# Golden Rules

Engineering excellence guidelines for Claude Code sessions.

## What is CLAUDE.md?

`CLAUDE.md` is a configuration file that Claude Code reads at the start of every session. It establishes coding standards, architectural preferences, and workflow expectations that Claude follows when assisting with software development.

## Purpose

These guidelines ensure Claude:

- **Maintains codebase integrity** - Works within existing architecture, preserves established patterns, and avoids unnecessary changes
- **Follows TDD practices** - Writes tests before implementation
- **Produces production-grade code** - With proper typing, error handling, and documentation
- **Avoids over-engineering** - Keeps solutions focused on what's actually needed
- **Delivers polished UI/UX** - Creates distinctive, accessible interfaces that avoid generic aesthetics

## Key Sections

| Section              | Focus                                                   |
| -------------------- | ------------------------------------------------------- |
| Core Rules           | Scope discipline, root cause analysis, code exploration |
| TypeScript Standards | Explicit types, build validation, linting               |
| Python Standards     | Type hints, modern 3.10+ syntax, quality tools          |
| Directory Layout     | Standard project structure conventions                  |
| Code Organization    | 200-line file limit, single responsibility              |
| UI/UX Excellence     | Distinctive design, accessibility, interaction polish   |
| Excellence Mandate   | Completion criteria and quality standards               |

## Usage

Place `CLAUDE.md` in your project root or `~/.claude/CLAUDE.md` for global defaults. Claude Code automatically reads these files at session start.

## Customization

Fork this repository and modify the guidelines to match your team's standards. The file uses XML-style tags for organization, which Claude parses to understand rule priorities and categories.
