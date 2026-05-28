# /identify-skill

A generative Claude Code skill. Helps you find the highest-leverage thing in your current week, then writes a working skill for it.

Use it whenever you don't know what to automate next.

## Quick start

You'll be running it in under a minute.

1. **Copy and paste this into your terminal:**

   ```bash
   mkdir -p ~/.claude/skills/identify-skill && \
   curl -fsSL https://raw.githubusercontent.com/zjamesblake/claude-code-workspace-generator/main/identify-skill/SKILL.md \
     -o ~/.claude/skills/identify-skill/SKILL.md && \
   echo "Installed. Open Claude Code and type /identify-skill"
   ```

2. **Open Claude Code** in any folder.

3. **Type `/identify-skill`** in the chat. The interview starts.

That's it. The skill lives at the user level, so it works in every Claude Code session from now on, on every workspace.

## What it does

In one conversation, `/identify-skill`:

1. Asks a handful of recency questions ("what ate your time this week?", "what did you keep procrastinating on?")
2. Surfaces 5 to 10 candidate tasks
3. Scores each on time, energy, and value
4. Ranks them by leverage (no-value drains float to the top)
5. Walks you through the first three lifecycle steps (identify the output, reverse-engineer the path, map the steps) for the one you pick
6. Writes a new `~/.claude/skills/<name>/SKILL.md` you can invoke immediately

Every skill it produces has **closed-loop hooks** baked in. After every run, the skill asks you what could be better and offers to edit itself. Your skills get smarter every time you use them.

The generator does the same thing to itself.

## What to expect

- **First run:** budget 20 to 30 minutes
- **Repeat runs:** 5 to 10 minutes (it remembers)
- **Voice-to-text helps.** The Discover phase is a brain dump.
- Don't run it on day one. Run it after you've felt a week of real friction.

## What it produces

Every run produces three things:

1. **A working skill** at `~/.claude/skills/<your-name>/SKILL.md`, invokable as `/<your-name>` immediately.
2. **A run history file** at `~/.claude/skills/identify-skill/runs/<date>_<name>.md`, so the next time you run `/identify-skill` it can pick up where you left off.
3. **Improvements to itself.** At the end of every run, `/identify-skill` asks what was clunky and edits its own instructions accordingly.

## Why this exists

This is the tool from the CC-02 video, **Building Your First Skill**. The video explains the framework (the lifecycle, closed-loop thinking, the high-leverage opportunity matrix). This is the tool that walks you through it.

If you haven't watched the video yet, the skill will still work. But the thinking underneath is what makes the tool worth using. Watch it.

## A word about leverage

The skill is opinionated about what's worth automating:

| | High value | Low / no value |
| --- | --- | --- |
| **High time + energy** | Tier 2: Leverage Builder. Real work that's draining. Automate to keep the value and reclaim the cost. | Tier 1: Eliminator. Pure overhead. Top priority. |
| **Low time + energy** | Polish or leave alone. | Stop doing it. |

The composite score is `(time + energy) × (2 if no value else 1)`. Tier 1 always ranks above Tier 2. Time and energy are your finite resources. Spending them on things that don't produce value is the highest-cost mistake. Fix that first.

## The closed-loop principle (do not remove from any skill)

Every skill `/identify-skill` produces ends with this block:

```markdown
## Closed-loop hooks (do not remove)

After this skill produces its output, before ending the session:

1. Ask the user: "What broke, was confusing, or could be better about this run?"
2. If the user identifies anything, propose specific edits to THIS file and apply them after confirmation.
3. If a step was unnecessary, cut it. If a step was missing, add it.
4. The first run of any skill is the worst it will ever produce. Iterate aggressively.
```

That's the engine. Don't strip it. It's what makes the difference between a skill that decays and a skill that compounds.

## Alternative install (clone the repo)

If you'd rather have the source locally:

```bash
git clone https://github.com/zjamesblake/claude-code-workspace-generator.git
mkdir -p ~/.claude/skills/identify-skill
cp claude-code-workspace-generator/identify-skill/SKILL.md ~/.claude/skills/identify-skill/SKILL.md
```

## Issues, ideas, contributions

Open an issue on GitHub or DM Zak. The skill itself will surface the feedback you give it. But if it's structural, the source lives here.
