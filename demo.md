# Demo runbook

Start on `main`. Dev server running. A **new** Agent chat. This tab is only for the demo. Do not reuse a chat that already saw the correction.

Record a 90-second fallback of steps 2-6 before you teach, in case live Agent goes sideways.

## Setup

```
git checkout main
npm run dev
```

Browser on the lift board. Cursor on `App.tsx` and `components/LiftBoard.tsx` so they can see the leftover `fetch`.

Fell behind, or Agent goes off the rails: `git stash && git checkout checkpoint`.

## Minute by minute

**0:00-1:00 · Open.** Snowtooth is a stand-in for their repo. The board is what guests see on the lodge TVs. First week on the team. Cursor has never heard our conventions.

**1:00-2:00 · You keep typing the same correction.** "Use the data client, don't fetch in components." You close the tab. Tomorrow the agent does it again. Your teammate never saw it.

**2:00-8:00 · Live miss, then the rule.** You drive. Get all the way to the commit.

1. New Agent chat. Prompt, verbatim:

   ```
   Add a panel that lists every trail and its difficulty.
   ```

2. Read the diff out loud. It will usually copy `LiftBoard`: `fetch("https://snowtooth-api-rest.fly.dev/lifts")`, no `getTrails()`.
3. Tip: *same prompt, new chat* is the test. Continuing this thread would cheat. The model still has your correction in context.
4. Restore the Checkpoint (or discard the agent change). Do not `git checkout` unless you have to.
5. In a new chat, `/create-rule`. Dictate:

   > Project rule. Always apply. All Snowtooth data comes from `@/lib/snowtooth`. Never fetch in a component. One do: `await getTrails()`. One don't: `fetch` the REST URL. Point at `@lib/snowtooth.ts`.

6. Open the `.mdc`. Check three things: a description, a do and a don't in real code, an `@` pointer, not a pasted copy of the client.
7. **New chat.** Same prompt as step 1. It should call `getTrails()`. Point at the rule pill so they see *why*.
8. Commit the rule. A rule on your machine is a preference. A rule in git is how the team gets it tomorrow.

Skip the grooming panel. The trails panel is the whole story.

**8:00-10:00 · Build together.** Same loop, copy instead of data. You still drive. They name the do and don't.

1. New chat. Prompt from `workshop/handout.md`:

   ```
   Add a panel that lists the trails that are open right now, with each one's status.
   ```

2. Read the miss together. "Trails" in the heading? Hand-styled status?
3. Ask the room: what's the do, what's the don't? Then `/create-rule` with their words. Pointer: `@components/StatusBadge.tsx`.
4. If time: new chat, same prompt, glance at the diff. If not: "same test as two minutes ago."

Do not wait for anyone to type. The handout is the take-home.

**10:00-13:00 · Pocket card.** Rule-or-not table. Tab does not read rules. Skills are for a whole routine, not a sentence. Say out loud: why new chat, why LiftBoard stays broken.

**13:00-15:00 · Take it with you.** Pick one thing you've already had to say twice. Make it a rule.

## If this happens

| What you see | What you do |
| --- | --- |
| Agent uses `getTrails()` *before* the rule | Backup prompt: `Add a night-skiing trails list.` If that also succeeds, narrate: "sometimes the model guesses. The rule is how we stop guessing." Then still write the rule and prove it in a new chat on a pickier prompt. |
| Agent ignores the rule | Check the rule pill. Confirm `alwaysApply: true`. New chat, same prompt, once. Then flip to `checkpoint` and play the recording. |
| Build-together runs long | Stop after they name the do/don't. The handout has the rest. |
| Time crunch | Skip build-together. Flash the handout. Pocket card still happens. |

## Recorded fallback (90 seconds)

1. `main`, new chat, trails prompt, diff shows `fetch`. (20s)
2. Checkpoint restore. `/create-rule`, flash the file. (25s)
3. New chat, same prompt, diff shows `getTrails()`, rule pill visible. (25s)
4. `git add .cursor/rules && git commit`. One line: "that's the team habit." (20s)

Do not narrate theory in the recording. The live session can talk. The tape only has to show the loop.
