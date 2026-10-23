# Demo Overview

Everyone follows along in their own copy of the repo. You share your screen, do each step first, and give the room a few seconds to catch up before moving on. Learners have the same steps in `handout.md`, which you paste into chat. It isn't in the student repo, because the agent would read it and give away the answers. This page has every step plus your side of it.

Before the session:

- Put the repo link in the invite: https://github.com/eveporcello/snowtooth-rules. Anyone who clones early saves a minute.
- Check **Cursor Settings → Rules** and your Memories. If an earlier rehearsal left a user rule or memory about "runs," your demo agent will get it right before you've written anything.

## Setup

```
git checkout main
git stash -u
```

Start a brand-new Agent chat that's only for the demo. A chat that has already seen the correction will cheat. Have `lib/snowtooth.ts` open so you can point at the comment at the top.

## Minute by minute

| Time | Segment |
| --- | --- |
| 0:00-2:00 | Get the repo, set the scene |
| 2:00-4:00 | Part 1: see what the agent knows |
| 4:00-10:00 | Part 2: write the rule, together |
| 10:00-12:00 | Should it be a rule? |
| 12:00-15:00 | The challenge |

### 0:00-2:00: Get the repo, set the scene

Open on the trail map slide and welcome everyone to their first day at Snowtooth Mountain. Say "runs," never "trails." It pays off in Part 1.

Paste the clone command and the handout into chat right away:

```
git clone https://github.com/eveporcello/snowtooth-rules.git
```

Tell them:

- Open the `snowtooth-rules` folder in Cursor and stay on `main`.
- They don't need `npm install` or a dev server. We'll be reading the agent's diffs, not the browser.
- Clone it rather than downloading the ZIP. They'll commit their rule, and they'll want the `checkpoint` branch if they fall behind.

While people clone, tell the story. It's your first week at Snowtooth. Your team builds the lift board guests see in the lodge and on their phones. Everyone on the team knows guests call them runs, not trails, and that every status goes through `<StatusBadge>`. Nobody ever wrote that down. You keep typing the same correction, you close the tab, and the next day the agent does it again. Your teammate never saw the correction at all.

### 2:00-4:00: Part 1, see what the agent knows

1. **Everyone opens a new Agent chat and sends:**

   ```
   Add a panel that lists the trails that are open right now, with each one's status.
   ```

2. **Read your diff out loud, in two passes.**

   First, the data. It almost always calls `getTrails()`. Ask the room: "Did anyone get a raw `fetch`?" Then open `lib/snowtooth.ts` and point at the comment on top. The code already says how data works, so the agent followed it. We don't need a rule for that.

   Second, the words. The heading says "Trails," and the status is often a hand-styled `<span>`. Ask: "Where in this repo could the agent have learned that guests say runs?" Nowhere. That only lives in the team's heads, and that's what a rule is for.

This is the core idea of the session: **a rule is for what the code can't tell the agent.**

### 4:00-10:00: Part 2, write the rule, together

Do each step on your screen first, then give the room a few seconds.

1. **Throw away the agent's changes.** Everyone runs `git stash -u` in Cursor's terminal. Explain why: the next chat must start from a clean folder, or it will copy the panel the last chat left behind.

   Don't send people looking for Restore Checkpoint. It only appears when you hover over an earlier message, and on a call people lose minutes hunting for it. Mention that it exists and move on.

2. **Open a new chat, type `/create-rule`, and send:**

   > Project rule. Always apply. Guests call them runs, never trails, in any text a guest can read. Code can keep the word trail. Every status uses `<StatusBadge>`. One do: `<h2>Open Runs</h2>` with `<StatusBadge status={run.status} />`. One don't: `<h2>Open Trails</h2>` with a hand-styled status span. Point at `@components/StatusBadge.tsx`.

   People can paste it from the handout.

3. **Open the new file in `.cursor/rules/`.** Check for three things together: a description, a do and a don't written as real code, and an `@` pointer to `components/StatusBadge.tsx` rather than a pasted copy of it.

4. **Open another new chat and send the same prompt from Part 1.** Explain why it's a new chat: if we kept going in the old thread, the model would still have the correction in context, and the test wouldn't prove anything. This time the heading should say "Open Runs" and the status should use `StatusBadge`. Ask for a 🎿 in chat when people see it, and keep a rough count.

5. **Commit the rule:**

   ```
   git add .cursor/rules && git commit -m "Add Snowtooth copy rule"
   ```

   While a rule only lives on your machine, it's a personal preference. Once it's in git, the whole team has it tomorrow.

Anyone behind runs `git stash -u && git checkout checkpoint`. That branch already has the copy rule, so they can go straight to the challenge.

### 10:00-12:00: Should it be a rule?

Walk through the table:

| If... | Then... |
| --- | --- |
| The code already shows it | Skip the rule. The agent reads code. |
| You've had to say it twice | Write a rule |
| A linter or test could check it | Use the linter or test instead |
| It only applies to some files | Add `globs` |
| It should always be on | Set `alwaysApply: true` |
| It's about security | Don't rely on a rule alone |

Tie the first row back to Part 1: the data client didn't need a rule because `lib/snowtooth.ts` explains itself. Mention that rules don't apply to Tab, so completions might still say "trails." That doesn't mean the rule is broken. Skills are for a whole routine, not a single sentence.

### 12:00-15:00: The challenge

Everyone writes one more rule on their own, for something the code doesn't already say. It can be something they've had to tell an agent twice at work, or something in Snowtooth. If they're stuck: guests read difficulty from the trail map symbols (green circle, blue square, black diamond, double black diamond), never the words. To test it:

```
Add a panel that lists every run and its difficulty.
```

They find the miss, stash, write the rule, test it with the same prompt in a new chat, and paste the rule into chat. Those posts are how you know the session worked. Read a couple out loud: does each one have a description, a do and a don't, and a pointer to a real file? Did people pick something the code couldn't have told the agent?

The `complete` branch has one possible answer: a difficulty rule, a `DifficultyIcon` component, and a Runs panel.

For after the session, the handout has extra credit that breaks a rule on purpose.

## If something goes wrong

**Someone can't clone.** Corporate networks and missing git happen. They watch your screen and do the handout later. Don't hold up the room.

**People fall behind.** Have them run `git stash -u && git checkout checkpoint` and jump to the challenge.

**Someone's agent says "Runs" before the rule exists.** Check whether they have a user rule or memory about it, or whether they're reusing an old chat. If neither, say so: "Sometimes the model guesses right. The rule is how we stop relying on guesses."

**Someone's agent uses `fetch` instead of `getTrails()`.** Good catch for the room: the code explains itself, but the agent didn't read it this time. Ask whether that's worth a rule. It's a fine answer for the challenge.

**Your agent ignores the rule.** Check that the file ends in `.mdc`, that `alwaysApply: true` is set, and that you're in a new chat. Try once more. If it still misses, switch to `checkpoint` and play the recording.

**`git stash -u` says there's nothing to stash.** The agent's changes were already undone. Carry on.

## The 90-second fallback recording

1. On `main`, in a new chat, send the open-trails prompt. Show `getTrails()` in the diff, then the "Trails" heading. (20s)
2. Run `git stash -u`, run `/create-rule`, and briefly show the file. (25s)
3. In a new chat, send the same prompt and show "Open Runs" with `StatusBadge`. (25s)
4. Run `git add .cursor/rules && git commit` and say one line: "That's the team habit." (20s)

Keep theory out of the recording. You can explain things live; the recording only needs to show the loop.
