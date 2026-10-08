# Installing these skills

You were asked to install the skills from this repository. Pick the path that matches your harness.

## Claude Code

1. Run `claude plugin marketplace add smaginweb/skills`.
2. Run `claude plugin install smaginweb-skills@smaginweb`.
3. Tell the user to restart Claude Code and try `/plain-report`.

## Other agents

1. Run `npx -y skills add smaginweb/skills -g -y -a <your agent name>`.
2. If that fails, copy `skills/plain-report` and `skills/lean-comments` into your skills folder (see INSTALL.md).

## Rules

- Do not edit the user's `CLAUDE.md` or `AGENTS.md` unless they ask for always-on mode.
- Finish with one short report: what was installed, where, and how to try it.
