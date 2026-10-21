# Lab · Snowtooth Copy Rule

> `main` or `checkpoint` if you fell behind · new Agent chat · about 4 minutes

It's your first week on the Snowtooth lift board team. Marketing just emailed: guests call them **runs**, never "trails," and every status shows up in a `<StatusBadge>`, never a hand-styled span.

1. New Agent chat. Send:

   ```
   Add a panel that lists the trails that are open right now, with each one's status.
   ```

   Read the diff. Does it say "trails" anywhere a guest will see? Does it use `StatusBadge`?

2. Restore the Checkpoint (don't `git checkout` unless you have to). Write `.cursor/rules/snowtooth-copy.mdc` — or type `/create-rule` and dictate it. You want a description, one do, one don't, and a pointer to `@components/StatusBadge.tsx`.

3. **New chat.** Same prompt. Check the diff again.

4. Commit the rule. That's how the next person gets it.

**Done:** a fresh chat produces a panel headed "Open Runs" that uses `StatusBadge`. Drop a 🎿 in chat.

## Stretch: break something on purpose

- Replace your rule with `Write good, consistent code.` Rerun. What happened, and why?
- Delete the description and leave no globs. When does the rule apply now?
- Add `globs: components/**/*.tsx`. Ask for a change in `lib/`. Does the rule show up?

## Rule or not?

| If... | Then... |
| --- | --- |
| You've said it twice | Write a rule |
| A linter or test can check it | Use the linter or test |
| It only applies to some files | Add `globs` |
| It must always be on | `alwaysApply: true` |
| It's about security | Never a rule alone |

Rules do not apply to Tab. Completions may still say "trails." That's not the rule failing.

Reference: [Cursor docs: Rules](https://cursor.com/docs/rules)
