# Snowtooth Rules

This is a 15-minute workshop for developers who are new to using Cursor. We want them to leave with one habit: when the agent keeps getting a team convention wrong, write it down as a rule instead of correcting it again.

## How the session runs

Everyone works in their own copy of the repo while we follow along on a shared screen.

| Time | Segment | What happens |
| --- | --- | --- |
| 0:00-2:00 | Get the repo | Everyone clones it and opens it in Cursor while we set up the story. |
| 2:00-8:00 | Data rule, together | We go step by step, with each step shown on screen first: see the miss, write the rule, test it in a new chat, commit. |
| 8:00-11:00 | Copy rule, on their own | The room names the do and don't, then everyone runs the loop. 🎿 in chat when it works. |
| 11:00-13:00 | Should it be a rule? | Walk through when to use a rule, a linter, or globs. |
| 13:00-15:00 | Challenge | Everyone writes one rule on their own and pastes it into chat. |

Anyone who falls behind switches to the `checkpoint` branch and picks up at the copy rule.

## What people should be able to do afterward

1. Notice when the agent makes the same mistake twice, and recognize that the fix is usually a missing rule, not a better prompt.
2. Write a project rule with a description, one do, one don't, and an `@` pointer to the real file.
3. Test it in a new chat with the same prompt, then commit it so the rest of the team gets it too.

By the end, a fresh chat should produce an Open Runs panel that uses `<StatusBadge>`.

## What we're leaving out

Fifteen minutes only has room for this one loop, so a lot stays out:

- **Skills.** A skill is a whole workflow. Skills get their own session.
- **User rules, Team rules, and `AGENTS.md`.** Same idea at a different scope. One project rule is plenty for today.
- **Plan, Ask, Tab, Browser, and Bugbot.** All useful, but they solve different problems. Today is only about getting the next chat to behave.
- **Fixing `LiftBoard`.** Rules shape what the agent writes next. They aren't a reason to rewrite old code.
- **Running the app.** The agent's mistakes show up in the diff, so nobody needs `npm install` or a dev server. That's one less thing to go wrong in the first two minutes.
- **A student website.** We built a landing page at [snowtooth-mountain.vercel.app](https://snowtooth-mountain.vercel.app/), but handing people a site and a repo is one link too many. We share the repo and paste the handout into chat.
- **Workshop notes in the student repo.** The handout, these notes, and the deck live in `snowtooth-rules-teacher-guide`. When they were inside `snowtooth-rules`, the agent read them and handed students the answers.
- **Apply Intelligently.** It's too unpredictable to rely on live, so we use `alwaysApply: true` and talk through the tradeoff.

## How we'll know it worked

At the end, everyone gets a small challenge: write one rule on their own and paste it into chat. It can be for something they've had to tell an agent twice at work, or something in the Snowtooth repo. Anyone who's stuck can use the Mountain Time convention in `lib/time.ts`, which doesn't have a rule yet.

What people post tells us whether the session worked. If their rules have a description, a do and a don't, and a pointer to a real file, they can write one without being walked through it. If the conventions they picked are the kind of thing a rule is good for, they understood when to reach for one.

Along the way, the 🎿 posts during Part 2 tell us whether people are keeping up.
