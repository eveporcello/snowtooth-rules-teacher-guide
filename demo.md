# Demo runbook

Start on `main`. Dev server running. A **new** Agent chat. This tab is only for the demo. Do not reuse a chat that already saw the correction.

Record a 90-second fallback of steps 2–6 before you teach, in case live Agent goes sideways.

## Setup

```
git checkout main
npm run dev
```

Browser on the lift board. Cursor on `App.tsx` and `components/LiftBoard.tsx` so they can see the leftover `fetch`.

Fell behind, or Agent goes off the rails: `git stash && git checkout checkpoint`.

## Minute by minute

**0:00–1:00 · Open.** Snowtooth is a stand-in for their repo. The board is what guests see on the lodge TVs. First week on the team. Cursor has never heard our conventions.

**1:00–2:00 · The Monday problem.** You’ve already typed “use the data client, don’t fetch in components” twice this week. Closing the chat wipes it. A teammate never saw it.

**2:00–6:30 · Live miss, then the rule.**

1. New Agent chat. Prompt, verbatim:

   ```
   Add a panel that lists every trail and its difficulty.
   ```

2. Read the diff out loud. It will usually copy `LiftBoard`: `fetch("https://snowtooth-api-rest.fly.dev/lifts")`, no `getTrails()`.
3. Tip: *same prompt, new chat* is the test. Continuing this thread would cheat. The model still has your correction in context.
4. Restore the Checkpoint (or discard the agent change). Do not `git checkout` unless you have to.
5. In a new chat, `/create-rule`. Dictate:

   > Project rule. Always apply. All Snowtooth data comes from `@/lib/snowtooth`. Never fetch in a component. One do: `await getTrails()`. One don’t: `fetch` the REST URL. Point at `@lib/snowtooth.ts`.

6. Open the `.mdc`. Check three things: a description, a do and a don’t in real code, an `@` pointer, not a pasted copy of the client.
7. **New chat.** Same prompt as step 1. It should call `getTrails()`. Point at the rule pill so they see *why*.
8. Optional second prompt, only if you have time: `Add the grooming report too.` Same client.
9. Commit the rule. Say this: a rule on your machine is a preference. A rule in git is how the team gets it tomorrow.

**6:30–11:00 · Lab.** Point at `workshop/handout.md`. Do not live-debug. Walk the room.

**11:00–13:30 · Pocket card.** Rule-or-not table. Tab does not read rules. Skills are for a whole routine, not a sentence.

**13:30–15:00 · Monday.** Pick one thing you’ve said twice. Make it a rule before standup.

## If this happens

| What you see | What you do |
| --- | --- |
| Agent uses `getTrails()` *before* the rule | Backup prompt: `Add a night-skiing trails list.` If that also succeeds, narrate: “sometimes the model guesses. The rule is how we stop guessing.” Then still write the rule and prove it in a new chat on a pickier prompt. |
| Agent ignores the rule | Check the rule pill. Confirm `alwaysApply: true`. New chat, same prompt, once. Then flip to `checkpoint` and play the recording. |
| Rule file is vague (`Write good code`) | Perfect teaching moment. Don’t fix it for them. Ask what the agent can actually *do* with that sentence. |
| Time crunch | Skip the grooming panel. The trails panel is the whole story. |
| Lab runs long | Pocket card becomes 45 seconds. The table is in the handout. |

## Recorded fallback (90 seconds)

1. `main`, new chat, trails prompt, diff shows `fetch`. (20s)
2. Checkpoint restore. `/create-rule`, flash the file. (25s)
3. New chat, same prompt, diff shows `getTrails()`, rule pill visible. (25s)
4. `git add .cursor/rules && git commit`. One line: “that’s the team habit.” (20s)

Do not narrate theory in the recording. The live session can talk. The tape only has to show the loop.
