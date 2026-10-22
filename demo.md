# Demo Overview

Everyone follows along in their own copy of the repo. You share your screen, do each step first, and give the room a few seconds to catch up before moving on. The steps people follow are in `workshop/handout.md`. This page is your side of it.

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

Paste the clone command and the link to `workshop/handout.md` into chat right away:

```
git clone https://github.com/eveporcello/snowtooth-rules.git
```

Tell them to open the folder in Cursor and stay on `main`. They don't need `npm install`.

While people clone, tell the story. Snowtooth stands in for their own repo, and the board is what guests see on the TVs in the lodge. It's your first week on the team, and you keep typing the same correction: "Use the data client, don't fetch in components." You close the tab, and the next day the agent does it again. Your teammate never saw the correction at all.

### 2:00-8:00: The data rule, together

Walk through Part 1 of the handout with everyone.

1. Send the trails prompt in your chat and have everyone send it in theirs. Read your diff out loud, then ask: "Who got `fetch`? Who got `getTrails()`?" Expect a mix.
2. Explain why the test will be the same prompt in a new chat. If we kept going in this thread, the model would still have the correction in context, and the test wouldn't prove anything.
3. Restore Checkpoint. Say clearly that this is Cursor's undo button, not the `checkpoint` branch. People new to Cursor mix those up.
4. New chat, `/create-rule`, and the dictation from the handout. People can paste it.
5. Open the `.mdc` file and check for three things: a description, a do and a don't written as real code, and an `@` pointer to the client rather than a pasted copy of it.
6. New chat, same prompt. It should call `getTrails()`. Point at the rule in the chat's context so people can see why.
7. Commit. While a rule only lives on your machine, it's a personal preference. Once it's in git, the whole team has it tomorrow.

Skip the grooming panel. The trails panel tells the whole story.

### 8:00-11:00: The copy rule, their turn

Point everyone at Part 2. Before anyone writes the rule, ask the room what the do and don't should be, and type their answer into chat so anyone who's behind can copy it. Then let them run it.

Ask for a 🎿 in chat when a fresh chat builds "Open Runs" with `StatusBadge`, and keep a rough count. That count is your in-room check.

### 11:00-13:00: The pocket card

Walk through the "Should it be a rule?" table. Mention that Tab doesn't read rules, and that skills are for a whole routine, not a single sentence. Say out loud why we keep opening new chats and why `LiftBoard` stays broken.

### 13:00-15:00: Send them off

Ask everyone to pick one thing they've already had to tell the agent twice and turn it into a rule in their own repo.

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
