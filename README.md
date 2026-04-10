# odoo-skills

A collection of Odoo skills to use with Claude Code, Gemini, or Codex.

## Installation

Clone into your Claude Code skills directory:

```bash
git clone git@github.com:andg-odoo/odoo-skills.git ~/.claude/skills/odoo-skills
```

Then symlink the skills you want:

```bash
ln -s ~/.claude/skills/odoo-skills/coverage ~/.claude/skills/coverage
```

## Skills

### `/coverage <module_name>`

Run test coverage analysis for an Odoo module. Finds the module, picks the right test database, runs `coverage` with branch analysis, and generates both a terminal summary and an HTML report.

**Prerequisites:** Your `CLAUDE.md` should define Odoo source repo paths, the path to `odoo-bin`, and a command to list test databases.

## Adding new skills

Each skill lives in its own directory with a `SKILL.md` file. See the [Claude Code docs](https://docs.anthropic.com/en/docs/claude-code/skills) for the skill file format.
