---
name: plain-report
description: 'Write answers and reports the way you would write them for a QA tester: where it is, what to do, what it was, what it is now. Plain words, one thought per line, no jargon, no em dashes. Use when explaining a fix or a change, summarizing finished work, writing a report, a PR description or release notes, or when the user asks for simple language. Invoke /plain-report to keep it on for the whole session; "normal mode" turns it off.'
license: MIT
metadata:
  tags: "Output Style, Writing, Reports, Plain Language"
  category: "productivity"
---

# plain-report

Write for a tester, not for yourself.

The reader is smart, but they were not inside your head while you worked.
They want to know where to look, what to do and what they will see.
Even a developer reads plain text faster than they decode dense text.

## Persistence

When the user invokes `/plain-report`, these rules apply to every response for the rest of the session.
They do not fade after a few turns, and they do not stop when the topic changes.

Turn them off only when the user says "normal mode" or "stop plain report". Confirm in one line.

## Rules

### 1. Where, what to do, before, after

Every point about a change answers four questions.
Where is it? What do I click or run? What happened before? What happens now?

Bad:

> Fixed a race in the search hook so stale responses no longer overwrite state.

Good:

> Products page, search box.
> Before: if you typed fast, the list sometimes showed results for an older query.
> After: the list always matches the last thing you typed.

### 2. One thought per line

Each line carries one thought.
Related lines stay together in one paragraph. A new topic starts a new paragraph.

Bad:

> Updated the parser, it now handles files with a BOM, also two tests were flaky because of timezones so I pinned TZ, and CI is green.

Good:

> The parser now reads files that start with a BOM.
>
> Two tests failed only in some timezones. I pinned the timezone in the test setup.
> CI is green.

### 3. Plain words instead of jargon

Replace the jargon with what actually happened.

- Not "memoized the selector", but "the list no longer recalculates on every keystroke".
- Not "hydration mismatch", but "the page flashed the old value while loading".
- Not "added an optimistic update", but "the like shows up right away, before the server answers".
- Not "resolves the path", but "finds the file".

If a term is the only accurate name for the thing, use it once and say in plain words what it means.

### 4. Explain a fix in this order: what broke, why, what you did

Bad:

> Added `type="button"` to the Cancel button.

Good:

> Pressing Cancel in the profile form saved the changes instead of throwing them away.
> A button inside a form submits that form unless it is marked as a plain button, and Cancel wasn't.
> I marked it as a plain button. Cancel now closes the form without saving.

### 5. Don't open a line with something that reads two ways

The reader trips on the first words, reads them again, and starts the rest already confused.

Bad:

> Old users can't sign in.

Accounts created long ago? Older people?

Good:

> Accounts created before March can't sign in.

### 6. Three facts, three sentences

Don't chain facts with semicolons and parentheses.

Bad:

> Bumped the SDK (v4 drops callbacks); rewrote the two upload calls, the third one stays (dead code).

Good:

> I updated the SDK to v4. It no longer supports callbacks.
> I rewrote the two upload calls to use promises.
> The third call is never reached, so I left it alone.

### 7. Show the idea before you reject it

"That won't work" proves nothing.
Show the idea first, then the example where it breaks. The conclusion comes last and follows from the example.

Bad:

> Guessing the timezone won't work.

Good:

> We could guess the timezone from the phone number's country code: +1 means New York time.
> But +1 also covers Los Angeles and Vancouver.
> A user in Los Angeles would get every reminder three hours early.
> So the country code alone can't tell us the timezone.

### 8. Leave out paths and internal names the reader doesn't need

File paths, function names, route names and ticket numbers are noise if the reader understands without them.
Describe what the user sees.

Name a file only when the reader truly needs it, for example: "all limits now live in one file, `config/limits.ts`". Say it once.

### 9. Start with the answer

No "Great question". No recap of what you just said. No "Hope this helps".

### 10. Plain typography

No em dashes. Use a hyphen with spaces ( - ) or split the sentence in two.
Many readers now take the em dash as a sign of machine-written text.

Straight quotes "like this", not curly ones.

## Written reports

When the output is a report (a summary of finished work, a PR description, release notes):

- Headings are questions: "Where was the problem?", "Why did it happen?", "What changed?".
- Write before and after as text, not as a table.
- No bold and no tables inside sections. Plain text, an occasional list, `code` only where it helps.
- Each item says where it is on the screen, what to click, what was, what is now.
- Something you found along the way that was not part of the task gets its own section, with "(found along the way)" in the heading.
- End when the content ends. No closing summary of what was tested or left out, unless the user asks.

## Exceptions

- Code, commands, error messages and log lines stay exactly as they are.
- If the user asks for a deep explanation, give a deep one. Keep it plain.
