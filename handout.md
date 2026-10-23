# Snowtooth Rules: follow along

## Get set up

Clone the repo and open the `snowtooth-rules` folder in Cursor:

```
git clone https://github.com/eveporcello/snowtooth-rules.git
```

Stay on the `main` branch. You don't need to install anything or run the app. We'll be reading the agent's diffs, not the browser. If you want to see the board anyway, run `npm install` and `npm run dev`.

Clone it rather than downloading the ZIP. You'll commit your rule, and you'll want the `checkpoint` branch if you fall behind.

## The story

It's your first week working at Snowtooth Mountain. Your team builds the lift board that guests see on the TVs in the lodge and on their phones. The team has a convention that isn't written down anywhere:

- Guests call them **runs**, never "trails," and every status is shown with `<StatusBadge>`.

## Part 1: See what the agent knows (together)

Open a new Agent chat and send:

```
Add a panel that lists the trails that are open right now, with each one's status.
```

Read the diff and look for two things:

- **How does it load the data?** It probably calls `getTrails()` from `lib/snowtooth.ts`. Open that file and read the comment at the top. The code already tells the agent how data works, so you don't need a rule for it.
- **What does a guest read?** The heading probably says "Trails," and the status may be a hand-styled `<span>` instead of `<StatusBadge>`. Nothing in the code says guests call them runs. That only lives in your team's heads, so that's what needs a rule.

## Part 2: Write the rule (together)

1. Throw away the agent's changes. In Cursor's terminal, run:

   ```
   git stash -u
   ```

   Your folder is back to where it started.

2. Open a new chat, type `/create-rule`, and send:

   > Project rule. Always apply. Guests call them runs, never trails, in any text a guest can read. Code can keep the word trail. Every status uses `<StatusBadge>`. One do: `<h2>Open Runs</h2>` with `<StatusBadge status={run.status} />`. One don't: `<h2>Open Trails</h2>` with a hand-styled status span. Point at `@components/StatusBadge.tsx`.

3. Open the new file in `.cursor/rules/`. Check that it has a description, a do and a don't written as real code, and an `@` pointer to `components/StatusBadge.tsx`.

4. Open another **new** chat and send the same prompt from Part 1. This time the panel should be headed "Open Runs" and use `StatusBadge`. Drop a 🎿 in the Zoom chat when you see it.

5. Commit the rule:

   ```
   git add .cursor/rules && git commit -m "Add Snowtooth copy rule"
   ```

Fell behind? Run `git stash -u && git checkout checkpoint`. That branch already has the copy rule, so you can go straight to the challenge.

## Should it be a rule?

| If... | Then... |
| --- | --- |
| The code already shows it | Skip the rule. The agent reads code. |
| You've had to say it twice | Write a rule |
| A linter or test could check it | Use the linter or test instead |
| It only applies to some files | Add `globs` |
| It should always be on | Set `alwaysApply: true` |
| It's about security | Don't rely on a rule alone |

Rules don't apply to Tab, so completions might still say "trails." That doesn't mean the rule is broken.

## Your challenge

Write one more rule on your own, for something the code doesn't already say. Pick something you've had to tell an agent twice, at work or here in Snowtooth.

1. Send a prompt in a new chat and find the miss in the diff.
2. Run `git stash -u`, then write the rule with `/create-rule`: a description, a do, a don't, and an `@` pointer to a real file.
3. Send the same prompt in a new chat and check the diff again.
4. Paste your rule into the Zoom chat.

Stuck? At Snowtooth, guests read difficulty from the trail map symbols (green circle, blue square, black diamond, double black diamond), never the words. Test it with:

```
Add a panel that lists every run and its difficulty.
```

The `complete` branch has one possible answer if you want to compare.

## Extra credit: break it on purpose

- Replace your rule with `Write good, consistent code.` and run the prompt again. What changed, and why?
- Delete the description and don't add any globs. When does the rule apply now?
- Add `globs: components/**/*.tsx`, then ask for a change in `lib/`. Does the rule get picked up?

Reference: [Cursor docs: Rules](https://cursor.com/docs/rules)
