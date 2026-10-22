# Snowtooth Rules

This is a 15-minute workshop for developers who are a week or two into using Cursor. They already know React, so I'm not going to walk them through features. What I want them to leave with is one habit: when the agent keeps getting a team convention wrong, write it down as a rule instead of correcting it again.

## How the session runs

The repo is the only thing people need. We start by having everyone clone it and open it in Cursor, then we run the loop together, each person in their own editor: send a prompt, watch the agent get a convention wrong, write a rule, open a new chat to prove it works, and commit it. I share my screen and do each step first so nobody gets lost.

We go through it twice. The first time, for the data rule, I walk the room through every step. The second time, for the copy rule, people do it themselves, and the room decides what the do and don't should be. Anyone who falls behind can switch to the `checkpoint` branch and pick up from there.

## What people should be able to do afterward

1. Notice when the agent makes the same mistake twice, and recognize that the fix is usually a missing rule, not a better prompt.
2. Write a project rule with a description, one do, one don't, and an `@` pointer to the real file.
3. Test it in a new chat with the same prompt, then commit it so the rest of the team gets it too.

By the end, a fresh chat should produce an Open Runs panel that uses `<StatusBadge>`.

## What we're leaving out

Fifteen minutes only has room for this one loop, so a lot stays out:

- **Skills.** A skill is a whole workflow. "Guests say runs" is just a constraint. Skills get their own session.
- **User rules, Team rules, and `AGENTS.md`.** Same idea at a different scope. One project rule is plenty for today.
- **Plan, Ask, Tab, Browser, and Bugbot.** All useful, but they solve different problems. Today is only about getting the next chat to behave.
- **Fixing `LiftBoard`.** It stays broken on purpose. Rules shape what the agent writes next. They aren't a reason to rewrite old code.
- **Running the app.** The agent's mistakes show up in the diff, so nobody needs `npm install` or a dev server. That's one less thing to go wrong in the first two minutes.
- **Apply Intelligently.** It's too unpredictable to rely on live, so I'll use `alwaysApply: true` and mention the tradeoff.

## How I'll know it worked

At the end, everyone gets a small challenge: write one rule on their own and paste it into chat. It can be for something they've had to tell an agent twice at work, or something in the Snowtooth repo. Anyone who's stuck can use the Mountain Time convention in `lib/time.ts`, which doesn't have a rule yet.

What people post tells me whether the session worked. If their rules have a description, a do and a don't, and a pointer to a real file, they can write one without me walking them through it. If the conventions they picked are the kind of thing a rule is good for, they understood when to reach for one.

Along the way, the 🎿 posts during Part 2 tell me whether people are keeping up.
