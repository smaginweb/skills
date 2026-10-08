---
name: lean-comments
description: 'Keep code comments to the few that earn their place: a hidden reason, a workaround for a bug, a rule that is not visible from here, a race. No comments that retell the code, no JSDoc for its own sake, no file banners. Use whenever you write or edit code.'
license: MIT
metadata:
  tags: "Code Style, Comments, Clean Code"
  category: "engineering"
---

# lean-comments

Most comments repeat the code in worse words.
They go stale, and then they lie.

A comment earns its place only when the code can't say it:

- a hidden reason: why this way and not the obvious one;
- a workaround for a bug in a browser, a library or an API;
- a rule that is not visible from this spot;
- a race, or an order of events that matters.

Everything else goes.

## Rules

### 1. Don't retell the code

Bad:

```ts
// Filter active users
const active = users.filter((u) => u.active);
```

Good:

```ts
const active = users.filter((u) => u.active);
```

### 2. Rename instead of explaining

If you want to explain what a piece of code means, give it a name.

Bad:

```ts
// check if the user can edit
if (user.role === "admin" || user.id === doc.ownerId) {
```

Good:

```ts
const canEdit = user.role === "admin" || user.id === doc.ownerId;
if (canEdit) {
```

If the code needs a paragraph to be understood, simplify the code before you write the paragraph.

### 3. Comment the reason the code can't show

Good:

```ts
// `blur` fires before `click`. Keep focus on the input so the menu item still gets the click.
item.addEventListener("mousedown", (e) => e.preventDefault());
```

```ts
// Responses can arrive out of order. Drop any that is not for the latest query.
if (requestId !== latestRequestId) return;
```

```css
.sidebar {
  /* Grid items don't shrink below their content by default, and a long URL would stretch the column. */
  min-width: 0;
}
```

One or two sentences. Say why, not what.

### 4. No JSDoc for its own sake

Bad:

```ts
/**
 * Gets the user name.
 * @param user The user.
 * @returns The user name.
 */
function getUserName(user: User): string {
```

Good: no comment. The signature already says all of it.

Write a doc comment for a public API only when it adds what the types don't: units, side effects, what happens on bad input.

### 5. No file banners

No headers with the file name, the author, the date or a paragraph about the module.
Git knows the author and the date. The exports show what the module does.

### 6. In tests, the name is the comment

Bad:

```ts
test("works", () => {
  // empty cart should have zero total
```

Good:

```ts
test("empty cart has a zero total", () => {
```

### 7. Fit in

Write comments in the language and format the file already uses.
Don't add or rewrite comments in code you didn't touch.

## Before you write a comment

1. Can a better name say this? Rename.
2. Can simpler code say this? Simplify.
3. Would a reader who knows the language still get it wrong without this line? Then write it, in one sentence.
