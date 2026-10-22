# Snowtooth Rules: follow along

## Get set up

Clone the repo and open the `snowtooth-rules` folder in Cursor:

```
git clone https://github.com/eveporcello/snowtooth-rules.git
```

Stay on the `main` branch. You don't need to install anything or run the app. We'll be reading the agent's diffs, not the browser. If you want to see the board anyway, run `npm install` and `npm run dev`.

Clone it rather than downloading the ZIP. You'll commit your rules, and you'll want the `checkpoint` branch if you fall behind.

## The story

It's your first week on the Snowtooth lift board team. The board is what guests see on the TVs in the lodge and on their phones. The team has two conventions Cursor doesn't know about yet:

- All data comes from the client in `lib/snowtooth.ts`. Components never call `fetch` directly.
- Guests call them **runs**, never "trails," and every status is shown with `<StatusBadge>`.

## Part 1: The data rule (together)

1. Open a new Agent chat and send:

   ```
   Add a panel that lists every trail and its difficulty.
   ```

   Look at the diff. Does the new component call `fetch` directly, or does it use `getTrails()` from `lib/snowtooth.ts`?

2. Undo the change with **Restore Checkpoint** in the chat. That's Cursor's undo button, not the `checkpoint` branch.

3. Open a new chat, type `/create-rule`, and send:

   > Project rule. Always apply. All Snowtooth data comes from `@/lib/snowtooth`. Never fetch in a component. One do: `await getTrails()`. One don't: `fetch` the REST URL. Point at `@lib/snowtooth.ts`.

4. Open the new file in `.cursor/rules/`. Check that it has a description, a do and a don't written as real code, and an `@` pointer to `lib/snowtooth.ts`.

5. Open another **new** chat and send the same prompt from step 1. This time it should use `getTrails()`, and the rule should show up in the chat's context.

6. Commit the rule:

   ```
   git add .cursor/rules && git commit -m "Add Snowtooth data rule"
   ```

If your agent used `getTrails()` the first time, that's fine. Sometimes it guesses right. Write the rule anyway; it's how you stop relying on guesses.

## Part 2: The copy rule (your turn)

Same steps, a little faster. This time you decide what the do and don't should be.

1. Open a new chat and send:

   ```
   Add a panel that lists the trails that are open right now, with each one's status.
   ```

   Does the word "trails" show up anywhere a guest would see it? Is the status a hand-styled span instead of `StatusBadge`?

2. Restore Checkpoint. Then type `/create-rule` and describe the convention in your own words. Include a description, one do, one don't, and a pointer to `@components/StatusBadge.tsx`.

3. Open a **new** chat, send the same prompt, and check the diff again.

4. Commit the rule so the next person on the team gets it.

You're done when a fresh chat builds a panel headed "Open Runs" that uses `StatusBadge`. Drop a 🎿 in the Zoom chat when you get there.

Fell behind? Run `git stash && git checkout checkpoint`. That branch already has the data rule, so you can go straight to Part 2. The `complete` branch has both rules if you want to compare yours.

## Your challenge

Write one more rule on your own. Pick something you've had to tell an agent twice, at work or here in Snowtooth. If you need an idea: every time a guest sees should be shown in Mountain Time, using `formatMountainTime()` from `lib/time.ts`.

Write the rule, test it with the same prompt in a new chat, and paste your rule into the chat so we can see what you built.

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
