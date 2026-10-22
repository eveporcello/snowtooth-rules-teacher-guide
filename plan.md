# Snowtooth Rules

This is a 15-minute workshop for developers who are a week or two into using Cursor. They already know React, so I'm not going to walk them through features. What I want them to leave with is one habit: when the agent keeps getting a team convention wrong, write it down as a rule instead of correcting it again.

## How the session runs

I'll demo the data rule from start to finish: show the agent getting it wrong, write the rule, open a new chat to prove it works, and commit it. Then we spend about two minutes writing the copy rule together. I'm still the one typing, but the room tells me what the do and don't should be. The handout is for later, not quiet lab time.

## What people should be able to do afterward

1. Notice when the agent makes the same mistake twice, and recognize that the fix is usually a missing rule, not a better prompt.
2. Write a project rule with a description, one do, one don't, and an `@` pointer to the real file.
3. Test it in a new chat with the same prompt, then commit it so the rest of the team gets it too.

By the end, a fresh chat should produce an Open Runs panel that uses `<StatusBadge>`.

## What we're leaving out

Fifteen minutes is enough for one pass through the loop, so a lot stays out:

- **Skills.** A skill is a whole workflow. "Guests say runs" is just a constraint. Skills get their own session.
- **User rules, Team rules, and `AGENTS.md`.** Same idea at a different scope. One project rule is plenty for today.
- **Plan, Ask, Tab, Browser, and Bugbot.** All useful, but they solve different problems. Today is only about getting the next chat to behave.
- **Fixing `LiftBoard`.** It stays broken on purpose. Rules shape what the agent writes next. They aren't a reason to rewrite old code.
- **Apply Intelligently.** It's too unpredictable to rely on live, so I'll use `alwaysApply: true` and mention the tradeoff.

## How I'll know it worked

During the session, the diff says "Open Runs" and uses `StatusBadge`.

A week later:

- The team has committed at least one file under `.cursor/rules/`.
- Nobody has to start a feature request with "remember, we say runs."
