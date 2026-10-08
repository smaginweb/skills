# How to install

## Claude Code

Install:

```bash
claude plugin marketplace add smaginweb/skills
claude plugin install smaginweb-skills@smaginweb
```

Restart Claude Code and try `/plain-report`.

Update:

```bash
claude plugin marketplace update smaginweb
claude plugin update smaginweb-skills@smaginweb
```

Uninstall:

```bash
claude plugin uninstall smaginweb-skills
claude plugin marketplace remove smaginweb
```

## Any agent with skills support

```bash
npx skills add smaginweb/skills
```

It asks which agents to install into.

## By hand

Copy the folders from `skills/` into your agent's skills folder:

| Agent | Folder |
| --- | --- |
| Claude Code | `~/.claude/skills/` |
| Codex | `~/.codex/skills/` |
| Cursor | `~/.cursor/skills/` |
| OpenCode | `~/.config/opencode/skill/` |

```bash
git clone --depth 1 https://github.com/smaginweb/skills.git /tmp/smaginweb-skills
cp -R /tmp/smaginweb-skills/skills/plain-report ~/.claude/skills/
cp -R /tmp/smaginweb-skills/skills/lean-comments ~/.claude/skills/
```

## Always on

Skills load when the agent decides they fit, or when you call them.
To apply the rules to every answer, paste the snippet from the [Always on](README.md#always-on) section of the README into your `CLAUDE.md` or `AGENTS.md`.
