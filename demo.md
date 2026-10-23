# Demo Overview

Everyone follows along in their own copy of the repo. You share your screen, do each step first, and give the room a few seconds to catch up before moving on. Learners have the same steps in `handout.md`, which you share with them. It isn't in the student repo. This page has every step plus your side of it.

Before the session:

- Put the repo link in the invite: https://github.com/eveporcello/snowtooth-rules. Anyone who clones early saves a minute.
- Record a 90-second fallback of Part 1 in case your own agent doesn't cooperate live.

## Setup

```
git checkout main
```

Start a brand-new Agent chat that's only for the demo. A chat that has already seen the correction will cheat. Have `App.tsx` and `components/LiftBoard.tsx` open so people can see the leftover `fetch`.

## Minute by minute

### 0:00-2:00: Get the repo, set the scene

Open on the trail map slide and welcome everyone to their first day at Snowtooth Mountain. Say "runs," never "trails." It pays off in the copy rule later.

Paste the clone command and the contents of `handout.md` into chat right away:

```
git clone https://github.com/eveporcello/snowtooth-rules.git
```

Tell them:

- Open the `snowtooth-rules` folder in Cursor and stay on `main`.
- They don't need `npm install` or a dev server. We'll be reading the agent's diffs, not the browser.
- Clone it rather than downloading the ZIP. They'll commit their rules, and they'll want the `checkpoint` branch if they fall behind.

While people clone, tell the story. It's your first week working at Snowtooth Mountain. Your team builds the lift board that guests see on the TVs in the lodge and on their phones, and the team has two conventions Cursor doesn't know about yet:

- All data comes from the client in `lib/snowtooth.ts`. Components never call `fetch` directly.
- Guests call them **runs**, never "trails," and every status is shown with `<StatusBadge>`.

You keep typing the same correction: "Use the data client, don't fetch in components." You close the tab, and the next day the agent does it again. Your teammate never saw the correction at all.

### 2:00-8:00: Part 1, the data rule, together

Do each step on your screen first, then give the room a few seconds.

1. **Everyone opens a new Agent chat and sends:**

   ```
   Add a panel that lists every trail and its difficulty.
   ```

   Read your diff out loud. Does the new component call `fetch` directly, or does it use `getTrails()` from `lib/snowtooth.ts`? Ask the room: "Who got `fetch`? Who got `getTrails()`?" Expect a mix.

   Explain why the test will be the same prompt in a new chat. If we kept going in this thread, the model would still have the correction in context, and the test wouldn't prove anything.

2. **Undo the change with Restore Checkpoint in the chat.** Say clearly that this is Cursor's undo button, not the `checkpoint` branch. People new to Cursor mix those up.

3. **Open a new chat, type `/create-rule`, and send:**

   > Project rule. Always apply. All Snowtooth data comes from `@/lib/snowtooth`. Never fetch in a component. One do: `await getTrails()`. One don't: `fetch` the REST URL. Point at `@lib/snowtooth.ts`.

   People can paste it from the handout.

4. **Open the new file in `.cursor/rules/`.** Check for three things together: a description, a do and a don't written as real code, and an `@` pointer to `lib/snowtooth.ts` rather than a pasted copy of the client.

5. **Open another new chat and send the same prompt from step 1.** This time it should call `getTrails()`. Point at the rule in the chat's context so people can see why.

6. **Commit the rule:**

   ```
   git add .cursor/rules && git commit -m "Add Snowtooth data rule"
   ```

   While a rule only lives on your machine, it's a personal preference. Once it's in git, the whole team has it tomorrow.

If someone's agent used `getTrails()` the first time, that's fine. Sometimes it guesses right. They write the rule anyway; it's how we stop relying on guesses.

### 8:00-11:00: Part 2, the copy rule, their turn

Same steps, a little faster. This time the room decides what the do and don't should be.

1. **Everyone opens a new chat and sends:**

   ```
   Add a panel that lists the trails that are open right now, with each one's status.
   ```

   Look at the miss together. Does the word "trails" show up anywhere a guest would see it? Is the status a hand-styled span instead of `StatusBadge`?

2. **Restore Checkpoint.** Before anyone writes the rule, ask the room what the do and don't should be, and type their answer into chat so anyone who's behind can copy it. Then everyone types `/create-rule` and describes the convention in their own words, with a description, one do, one don't, and a pointer to `@components/StatusBadge.tsx`.

3. **Open a new chat, send the same prompt, and check the diff again.**

4. **Commit the rule** so the next person on the team gets it.

They're done when a fresh chat builds a panel headed "Open Runs" that uses `StatusBadge`. Ask for a 🎿 in chat when they get there, and keep a rough count. That count is your in-room check.

Anyone behind runs `git stash && git checkout checkpoint`. That branch already has the data rule, so they can go straight to Part 2. The `complete` branch has both rules if they want to compare.

### 11:00-13:00: The pocket card

Walk through the "Should it be a rule?" table:

| If... | Then... |
| --- | --- |
| You've had to say it twice | Write a rule |
| A linter or test could check it | Use the linter or test instead |
| It only applies to some files | Add `globs` |
| It should always be on | Set `alwaysApply: true` |
| It's about security | Don't rely on a rule alone |

Mention that rules don't apply to Tab, so completions might still say "trails." That doesn't mean the rule is broken. Skills are for a whole routine, not a single sentence. Say out loud why we keep opening new chats and why `LiftBoard` stays broken.

### 13:00-15:00: The challenge

Everyone writes one more rule on their own. It can be for something they've had to tell an agent twice at work, or something in Snowtooth. If they're stuck, suggest Mountain Time: every time a guest sees should go through `formatMountainTime()` in `lib/time.ts`, and nothing enforces that yet. To test a Mountain Time rule:

```
Add a panel that shows when each run was last groomed.
```

They write the rule, test it with the same prompt in a new chat, and paste the rule into chat. Those posts are how you know the session worked. Read a couple out loud: does each one have a description, a do and a don't, and a pointer to a real file? Did people pick something a rule is actually good for?

For after the session, the handout has extra credit that breaks a rule on purpose:

- Replace the rule with `Write good, consistent code.` and run the prompt again. What changed, and why?
- Delete the description and don't add any globs. When does the rule apply now?
- Add `globs: components/**/*.tsx`, then ask for a change in `lib/`. Does the rule get picked up?

## If something goes wrong

**Someone can't clone.** Corporate networks and missing git happen. They watch your screen for Part 1 and do the handout later. Don't hold up the room.

**People fall behind.** Have them run `git stash && git checkout checkpoint` and jump to Part 2.

**Some agents use `getTrails()` before the rule exists.** That's normal. Say so: "Sometimes the model guesses right. The rule is how we stop relying on guesses." If your own agent got it right, try the backup prompt, `Add a night-skiing trails list.`, so the room still sees a miss.

**Your agent ignores the rule.** Check that the rule shows up in the chat's context and that `alwaysApply: true` is set. Try one more new chat with the same prompt. If it still misses, switch to `checkpoint` and play the recording.

**Part 2 runs long.** Stop once the room has named the do and don't. The handout has the rest. Still do the pocket card.

## The 90-second fallback recording

1. On `main`, in a new chat, send the trails prompt and show the diff with `fetch`. (20s)
2. Restore Checkpoint, run `/create-rule`, and briefly show the file. (25s)
3. In a new chat, send the same prompt and show the diff with `getTrails()` and the rule in context. (25s)
4. Run `git add .cursor/rules && git commit` and say one line: "That's the team habit." (20s)

Keep theory out of the recording. You can explain things live; the recording only needs to show the loop.
