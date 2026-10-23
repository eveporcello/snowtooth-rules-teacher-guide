# Snowtooth Rules

This is a 15-minute workshop for professional developers who are new to Cursor. They already know git, React, and code review. They've used the Agent a little, and they've had to correct it more than once. We want them to leave with one habit: when the agent keeps getting a team convention wrong, write it down as a rule instead of correcting it again. And just as important, know when a rule isn't needed.

## How the session runs

Everyone works in their own copy of the repo while we follow along on a shared screen.

| Time | Segment | What happens |
| --- | --- | --- |
| 0:00-2:00 | Get the repo | Everyone clones it and opens it in Cursor while we set up the story. |
| 2:00-4:00 | See what the agent knows | One prompt. The agent loads data the right way because the code explains it, and writes "Trails" because nothing says guests call them runs. |
| 4:00-10:00 | Write the rule, together | Step by step, each step shown on screen first: reset, write the rule, test it in a new chat, commit. 🎿 in chat when it works. |
| 10:00-12:00 | Should it be a rule? | When to use a rule, a linter, globs, or nothing at all. |
| 12:00-15:00 | Challenge | Everyone writes one rule on their own and pastes it into chat. |

Anyone who falls behind switches to the `checkpoint` branch and picks up at the challenge.

## What people should be able to do afterward

1. Write a project rule with a description, one do, one don't, and an `@` pointer to the real file.
2. Test it in a new chat with the same prompt, then commit it so the rest of the team gets it too.
3. Explain the reasoning behind what should be in a rule and criteria for creating rules.

By the end, a fresh chat should produce an Open Runs panel that uses `<StatusBadge>`.

## What we're leaving out

Fifteen minutes only has room for this one loop, so a lot stays out:

- **A rule for the data client.** The first draft had people write "never fetch in a component." In rehearsal, the agent used `getTrails()` every time, because `lib/snowtooth.ts` says how data works. A rule that fixes nothing teaches the wrong lesson, so we kept the moment and turned it into the point: the code already said it.
- **Restore Checkpoint.** It only shows up when you hover over an earlier message, and people lose minutes hunting for it on a call. `git stash -u` resets everyone the same way and is a habit they already have.
- **Skills.** A skill is a whole workflow. Skills get their own session.
- **User rules, Team rules, and `AGENTS.md`.** Same idea at a different scope. One project rule is plenty for today.
- **Plan, Ask, Tab, Browser, and Bugbot.** All useful, but they solve different problems. Today is only about getting the next chat to behave.
- **Fixing `LiftBoard`.** Rules shape what the agent writes next. They aren't a reason to rewrite old code.
- **Running the app.** The agent's mistakes show up in the diff, so nobody needs `npm install` or a dev server. That's one less thing to go wrong in the first two minutes.
- **A student website.** We built a landing page at [snowtooth-mountain.vercel.app](https://snowtooth-mountain.vercel.app/), but handing people a site and a repo is one link too many. We share the repo and paste the handout into chat.
- **Workshop notes in the student repo.** The handout, these notes, and the deck live in `snowtooth-rules-teacher-guide`. When they were inside `snowtooth-rules`, the agent read them and handed students the answers.
- **Apply Intelligently.** It's too unpredictable to rely on live, so we use `alwaysApply: true` and talk through the tradeoff.

## How we'll know it worked

At the end, everyone gets a small challenge: write one rule on their own and paste it into chat. It can be for something they've had to tell an agent twice at work, or something in Snowtooth. Anyone who's stuck can use the difficulty convention: guests read the trail map symbols, never the words.

What people post tells us whether the session worked. If their rules have a description, a do and a don't, and a pointer to a real file, they can write one without being walked through it. If they picked something the code couldn't have told the agent, they understood when to reach for a rule.

Along the way, the 🎿 posts during Part 2 tell us whether people are keeping up.
