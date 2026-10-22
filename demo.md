# Demo Overview

Start on `main` with the dev server running and a brand-new Agent chat. Use that chat only for the demo. A chat that has already seen the correction will cheat.

Before the session, record a 90-second fallback of steps 2 through 6 in case the live agent doesn't cooperate.

## Setup

```
git checkout main
npm run dev
```

Have the lift board open in the browser, and have `App.tsx` and `components/LiftBoard.tsx` open in Cursor so people can see the leftover `fetch`.

If anyone falls behind, or the agent goes off the rails, run `git stash && git checkout checkpoint`.

## Minute by minute

### 0:00-1:00: Open

Snowtooth stands in for their own repo. The board is what guests see on the TVs in the lodge. Set the scene: it's your first week on the team, and Cursor doesn't know any of our conventions yet.

### 1:00-2:00: The correction you keep typing

"Use the data client, don't fetch in components." You say it, close the tab, and the next day the agent does it again. Your teammate never saw the correction at all.

### 2:00-8:00: Show the miss, then write the rule

You drive the whole way, right through to the commit.

1. Open a new Agent chat and send this prompt exactly:

   ```
   Add a panel that lists every trail and its difficulty.
   ```

2. Read the diff out loud. It usually copies `LiftBoard` and calls `fetch("https://snowtooth-api-rest.fly.dev/lifts")` instead of `getTrails()`.
3. Explain why the test is the same prompt in a new chat. If we kept going in this thread, the model would still have the correction in context, and the test wouldn't prove anything.
4. Restore the checkpoint, or discard the agent's change. Only use `git checkout` if you have to.
5. Open a new chat, type `/create-rule`, and dictate:

   > Project rule. Always apply. All Snowtooth data comes from `@/lib/snowtooth`. Never fetch in a component. One do: `await getTrails()`. One don't: `fetch` the REST URL. Point at `@lib/snowtooth.ts`.

6. Open the `.mdc` file and check for three things: a description, a do and a don't written as real code, and an `@` pointer to the client rather than a pasted copy of it.
7. Open another new chat and send the same prompt from step 1. This time it should call `getTrails()`. Point at the rule pill so people can see why.
8. Commit the rule. While it only lives on your machine, it's a personal preference. Once it's in git, the whole team has it tomorrow.

Skip the grooming panel. The trails panel tells the whole story.

### 8:00-10:00: Build one together

This is the same loop, but for wording instead of data. You're still typing; the room supplies the do and don't.

1. Open a new chat and send the prompt from `workshop/handout.md`:

   ```
   Add a panel that lists the trails that are open right now, with each one's status.
   ```

2. Look at what it got wrong together. Does the heading say "Trails"? Is the status styled by hand?
3. Ask the room what the do and don't should be, then run `/create-rule` using their words. Point it at `@components/StatusBadge.tsx`.
4. If there's time, open a new chat, rerun the same prompt, and take a quick look at the diff. If not, just say it's the same test we ran two minutes ago.

Don't wait for people to type along. They can work through the handout later.

### 10:00-13:00: The pocket card

Walk through the "Should it be a rule?" table. Mention that Tab doesn't read rules, and that skills are for a whole routine, not a single sentence. Say out loud why we keep opening new chats and why `LiftBoard` stays broken.

### 13:00-15:00: Send them off

Ask everyone to pick one thing they've already had to tell the agent twice and turn it into a rule.

## If something goes wrong

**The agent uses `getTrails()` before the rule exists.** Try the backup prompt: `Add a night-skiing trails list.` If that works too, say so: "Sometimes the model guesses right. The rule is how we stop relying on guesses." Then write the rule anyway, and prove it in a new chat with a pickier prompt.

**The agent ignores the rule.** Check that the rule pill is showing and that `alwaysApply: true` is set. Try one more new chat with the same prompt. If it still misses, switch to `checkpoint` and play the recording.

**Building together runs long.** Stop once the room has named the do and don't. The handout covers the rest.

**You're short on time.** Skip building together and just show the handout. Still do the pocket card.

## The 90-second fallback recording

1. On `main`, in a new chat, send the trails prompt and show the diff with `fetch`. (20s)
2. Restore the checkpoint, run `/create-rule`, and briefly show the file. (25s)
3. In a new chat, send the same prompt and show the diff with `getTrails()` and the rule pill visible. (25s)
4. Run `git add .cursor/rules && git commit` and say one line: "That's the team habit." (20s)

Keep theory out of the recording. You can explain things live; the recording only needs to show the loop.
