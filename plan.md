# Snowtooth Rules

15-minute workshop. Professional developers, first or second week of Cursor seats. They already ship React. They do not need a feature tour. They need the habit that stops the agent from arguing with team conventions.

**How it runs.** You demo the data rule (miss, write, new chat, commit). Then two minutes building the copy rule together: you drive, they name the do and don't. The handout is the take-home, not silent lab time.

## What people leave able to do

1. Spot a repeated agent miss as a missing rule, not a bad prompt.
2. Write a project rule with a description, one do, one don’t, and an `@` pointer to the real file.
3. Prove it in a **new chat** with the same prompt, then commit it so the next teammate gets it.

Done looks like: a fresh chat produces an **Open Runs** panel that uses `<StatusBadge>`.

## What we skip

This is 15 minutes. One loop: miss → encode → new chat → commit.

| We skip | Why |
| --- | --- |
| Skills | A skill is a workflow. “Guests say runs” is a constraint. That’s a later session. |
| User rules, Team rules, `AGENTS.md` | Same idea, different scope. One repo-local rule is enough today. |
| Plan, Ask, Tab, Browser, Bugbot | Different jobs. Today is “make the next chat behave.” |
| Fixing `LiftBoard` | Left broken on purpose. Rules are for next time, not a legacy rewrite. |
| Apply Intelligently as the live path | Too flaky live. We set `alwaysApply: true` and name the tradeoff. |

## How you know it worked

**In the room.** The diff says “Open Runs” and uses `StatusBadge`.

**Next week.**

- The team has committed at least one file under `.cursor/rules/`.
- The next feature request is not preceded by “remember, we say runs.”
