---
name: coverage
description: Run Odoo test coverage for a module. Use after finishing a task to measure test coverage, identify untested code paths, and generate an HTML report.
argument-hint: <module_name>
allowed-tools: Bash(coverage *) Bash(xdg-open *)
---

# Odoo Test Coverage

Run test coverage analysis for the Odoo module `$ARGUMENTS`.

## Prerequisites

This skill relies on the user's CLAUDE.md to define their Odoo environment. It should specify:
- **Odoo source repo paths** (community and enterprise) so the module can be located
- **Path to `odoo-bin`**
- **A command to list available test databases** and the naming convention used

Check CLAUDE.md for these details before proceeding.

## Steps

1. Determine the module path. Search the Odoo source repo paths from CLAUDE.md for a directory named `$ARGUMENTS`.
2. Find the correct database to run tests against. Use the DB listing command from CLAUDE.md and pick the one that matches the current branch version, or ask the user which DB to use.
3. Run coverage:

```
coverage run --branch \
  --source=<module_path> \
  <odoo-bin_path> -d <db_name> \
  --test-tags /$ARGUMENTS \
  --stop-after-init
```

4. Show the terminal report (excluding test files):

```
coverage report -m --omit='*/tests/*'
```

5. Generate the HTML report into `<module_path>/htmlcov/`:

```
coverage html --omit='*/tests/*' -d <module_path>/htmlcov
```

6. Open the HTML report with `xdg-open`.

7. Summarize the results: overall coverage percentage, files with lowest coverage, and the most significant untested lines/branches.

## Notes

- If 0 tests run, the tests are likely tagged `post_install` -- just use `--test-tags /$ARGUMENTS` without `-i` or `-u` flags to pick them up.
- Skip tests tagged `external` or `-standard` since those require live API credentials.
- `htmlcov/` is gitignored -- don't commit it.
