# Build together: the Snowtooth copy rule

> We'll do this together live in about two minutes. You can redo it afterward on `main`, or on `checkpoint` if you fell behind.

It's your first week on the Snowtooth lift board team, and marketing just sent an email: guests call them **runs**, never "trails," and every status should be shown with a `<StatusBadge>`, not a span styled by hand.

1. Open a new Agent chat and send:

   ```
   Add a panel that lists the trails that are open right now, with each one's status.
   ```

   Look at the diff. Does the word "trails" show up anywhere a guest would see it? Does it use `StatusBadge`?

2. Restore the checkpoint (only use `git checkout` if you have to). Then write `.cursor/rules/snowtooth-copy.mdc` yourself, or type `/create-rule` and dictate it. It should have a description, one do, one don't, and a pointer to `@components/StatusBadge.tsx`.

3. Open a **new** chat, send the same prompt, and check the diff again.

4. Commit the rule so the next person on the team gets it.

You're done when a fresh chat builds a panel headed "Open Runs" that uses `StatusBadge`. Drop a 🎿 in the chat when you get there.

## Extra credit: break it on purpose

- Replace your rule with `Write good, consistent code.` and run the prompt again. What changed, and why?
- Delete the description and don't add any globs. When does the rule apply now?
- Add `globs: components/**/*.tsx`, then ask for a change in `lib/`. Does the rule get picked up?

## Should it be a rule?

| If... | Then... |
| --- | --- |
| You've had to say it twice | Write a rule |
| A linter or test could check it | Use the linter or test instead |
| It only applies to some files | Add `globs` |
| It should always be on | Set `alwaysApply: true` |
| It's about security | Don't rely on a rule alone |

Rules don't apply to Tab, so completions might still say "trails." That doesn't mean the rule is broken.

Reference: [Cursor docs: Rules](https://cursor.com/docs/rules)
