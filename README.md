# skills

**Your agent writes like a good bug report. Your code stops narrating itself.**

Two small skills for Claude Code, Codex, Cursor and any agent that reads `SKILL.md`.

## Install

Paste into your agent:

```text
Install the skills from https://github.com/smaginweb/skills. Follow the repo's AGENTS.md.
```

Or in Claude Code:

```text
/plugin marketplace add smaginweb/skills
/plugin install smaginweb-skills@smaginweb
```

Or for any agent:

```bash
npx skills add smaginweb/skills
```

More options in [INSTALL.md](INSTALL.md).

## The skills

| Skill | What it does |
| --- | --- |
| [plain-report](skills/plain-report/SKILL.md) | Answers like a report for a QA tester: where, what to click, before, after. Plain words, one thought per line, no em dashes. |
| [lean-comments](skills/lean-comments/SKILL.md) | Comments only where the code can't speak: hidden reasons, workarounds, races. No JSDoc for its own sake. |

## plain-report

<table>
<tr>
<td width="50%">

### Before

> Great question! I looked into the issue, and it turns out the `useSearch` hook had a race condition: when `fetchResults` resolved out of order, the stale response would overwrite the state via `setResults`. I've refactored the hook to track the latest request ID with a ref (see `src/hooks/useSearch.ts`, lines 14-37) and memoized the debounced callback; the tests pass (except one flaky e2e test, unrelated). Hope this helps!

</td>
<td width="50%">

### After

> Products page, search box.
> Before: if you typed fast, the list sometimes showed results for an older query.
> After: the list always matches the last thing you typed.
>
> Answers from the server could arrive out of order, and an old one overwrote the new one.
> Now old answers are ignored.

</td>
</tr>
</table>

### The rules

Full text in [SKILL.md](skills/plain-report/SKILL.md).

1. Where, what to do, before, after.
2. One thought per line.
3. Plain words instead of jargon.
4. Explain a fix in order: what broke, why, what you did.
5. Don't open a line with something that reads two ways.
6. Three facts, three sentences.
7. Show the idea before you reject it.
8. Leave out paths and internal names the reader doesn't need.
9. Start with the answer.
10. No em dashes, no curly quotes.

Turn it on for the whole session with `/plain-report`. Say "normal mode" to turn it off.

The agent also picks it up by itself when it explains a change, sums up finished work or writes a PR description.

## lean-comments

<table>
<tr>
<td width="50%">

### Before

```ts
/**
 * Gets the visible items.
 * @param items The items.
 * @returns The visible items.
 */
function getVisible(items: Item[]) {
  // filter out hidden items
  return items.filter((i) => !i.hidden);
}

// check if the user can edit
if (user.role === "admin" || user.id === doc.ownerId) {
```

</td>
<td width="50%">

### After

```ts
function getVisible(items: Item[]) {
  return items.filter((i) => !i.hidden);
}

const canEdit = user.role === "admin" || user.id === doc.ownerId;
if (canEdit) {

// Responses can arrive out of order. Drop any that is not for the latest query.
if (requestId !== latestRequestId) return;
```

</td>
</tr>
</table>

A comment stays only when the code can't say it: a hidden reason, a workaround, a rule that is not visible from here, a race.

## Always on

Add this to your `CLAUDE.md` or `AGENTS.md`:

```markdown
## How to write answers

Write like a report for a QA tester: where it is, what to click or run, what it was, what it is now.
One thought per line. Plain words instead of jargon.
Explaining a fix: what broke, why, what you did.
Leave out file paths and internal names the reader doesn't need.
No em dashes, no curly quotes. No preamble, no recap.

## Code comments

Only where the code can't say it: a hidden reason, a workaround, a non-obvious rule, a race.
Rename or simplify instead of explaining. No JSDoc for its own sake.
```

## Tune it

Fork the repo, edit the `SKILL.md` files, then install from your fork:

```bash
claude plugin uninstall smaginweb-skills
claude plugin marketplace remove smaginweb
claude plugin marketplace add <your-username>/skills
claude plugin install smaginweb-skills@smaginweb
```

## License

[MIT](LICENSE)

Star it if you ever had to read your agent's summary twice.
