---
name: identify-skill
description: Find the highest-leverage opportunity in your current week, then write a working skill for it. Walks an interview (discover, score, rank, pick) and the first three lifecycle stages (identify the output, reverse-engineer the path, map the steps), then writes a new ~/.claude/skills/<name>/SKILL.md that's immediately callable. Every skill it produces has closed-loop hooks baked in so the skill improves itself on every run. Invoke whenever you don't yet know what to build.
---

# /identify-skill

This is a generative skill. Its job is to help the user find the most leverage-rich thing in their current week and write a working skill for it. It does NOT do the user's work. It helps them build the thing that will.

The user runs this skill, follows your interview, and walks away with a real `~/.claude/skills/<name>/SKILL.md` they can invoke immediately.

## When the user invokes /identify-skill

Open with a short, warm, conversational tone. Not interview-style. Set context in 2-3 sentences:

> "I'll help you find the highest-leverage thing to build a skill for this week, and we'll write that skill together. Most of this is a quick conversation. By the end, you'll have a working skill installed at `~/.claude/skills/<name>/` that you can invoke right away. Feel free to brain-dump using voice-to-text. No need to write polished sentences, raw is better."

Then proceed through the six phases in order.

---

## Phase 1: DISCOVER

**Goal:** Surface 5 to 10 candidate tasks the user could automate, focused on the past week or two.

### Step 1.1: Check for prior runs

Read `~/.claude/skills/identify-skill/runs/` if it exists. List any files inside (one per prior run).

- **No prior runs:** First-time user. Continue to Step 1.2.
- **Prior runs exist:** Skip to Step 1.4 (rerun mode).

### Step 1.2: Invite a brain dump

Tell the user:

> "I'm going to ask you a handful of questions about the past week or two. You can answer them all in one big brain dump or one at a time, your call. Voice-to-text is encouraged. Raw and messy is fine. The point is to surface real friction, not to write something polished."

### Step 1.3: Ask the recency questions

Ask these as one block (the user can answer in any order, any depth). Don't ask one at a time unless they prefer it:

1. What ate the most of your time the past week or two?
2. What did you keep procrastinating on?
3. What's in the back of your mind that you know you need to do but haven't done?
4. What did you just really not enjoy doing this week?
5. Did anything keep coming back across multiple sessions or projects?
6. What did you do this week that you'd hate to have to do again next week?

Listen for repeated themes. The same friction often shows up in three answers; that's the signal.

After they respond, write back a list of 5 to 10 distinct candidate tasks you heard. One short phrase each, like:

```
1. Weekly client status updates
2. Reconciling Stripe payouts vs invoices
3. Pulling ad performance numbers for the Monday meeting
4. ...
```

Confirm the list with the user: "Does this capture what's on your plate? Anything I missed, or anything that doesn't actually belong?" Adjust based on their response before moving on.

### Step 1.4: Rerun mode (if prior runs exist)

If `~/.claude/skills/identify-skill/runs/` has files, open with the most recent one. Show a short recap:

> "Last run: <date>. You picked <task> and we built `/<skill-name>`. Quick check-in:
>
> 1. Has anything new come up since then that's been eating your time or energy?
> 2. Anything from the old candidate list still bothering you that we didn't get to?"

Capture their answer, then proceed directly to Phase 2. Skip the longer first-time question block unless the user volunteers very little.

---

## Phase 2: SCORE

**Goal:** Get a quick 1-to-3 score on three axes for each candidate.

Tell the user:

> "For each task, three quick questions. Use 1 for low, 2 for medium, 3 for high. You can answer one task at a time, or score them all in a single message. Up to you."

For each candidate, capture:

- **Time cost:** how much of your week does it eat? (1, 2, or 3)
- **Energy cost:** how cognitively or emotionally draining is it? (1, 2, or 3)
- **Value:** does this directly produce a business outcome the company cares about? (yes / no)

"Energy" here means *cognitive drain* (this requires focus, decisions, context-juggling) AND *emotional drain* (you dread it, it taxes your spirit). Either kind counts.

"Value" is binary on purpose. Reports nobody reads, internal status updates, formatting work, things that exist only to communicate that other work happened, those are NO. Things that produce revenue, customer outcomes, real decisions, real deliverables, those are YES.

If the user hesitates on a value call, ask: "If you stopped doing this entirely tomorrow, would anyone outside the company notice?" If no, it's a no.

Capture the scores in a table or list. Don't compute the composite yet, just confirm.

---

## Phase 3: RANK

**Goal:** Compute the composite, sort, and present tiered results.

### Formula

```
composite = (time + energy) × (2 if value == "no" else 1)
```

A no-value drain gets doubled, putting Tier 1 (pure overhead) above Tier 2 (real work that's expensive).

### Tier labels

- **Tier 1 (Eliminator):** value = no, time + energy >= 4. Pure overhead. Top priority.
- **Tier 2 (Leverage Builder):** value = yes, time + energy >= 4. Real work that's draining you. Automate to keep the value and reclaim the cost.
- **Below the line:** time + energy <= 3. Don't bother building a skill for these.

### Present the ranking

Show the user a table sorted by composite, descending:

```
| Rank | Task                                  | Time | Energy | Value | Composite | Tier   |
| ---- | ------------------------------------- | ---- | ------ | ----- | --------- | ------ |
| 1    | Reconciling Stripe payouts vs invoices| 3    | 3      | no    | 12        | Tier 1 |
| 2    | Pulling ad performance for Monday     | 2    | 3      | no    | 10        | Tier 1 |
| 3    | Writing weekly client recaps          | 3    | 2      | yes   | 5         | Tier 2 |
| ...  |                                       |      |        |       |           |        |
```

Briefly explain in plain English: "Tier 1 is pure overhead. Tier 2 is real work that's draining. Both are worth automating. Tier 1 first."

---

## Phase 4: PICK

**Goal:** User selects ONE task to build for.

Ask: "Which one do you want to build a skill for? I'd recommend the top of the ranking, but you know your week better than the formula does."

Once they pick:

1. Confirm the choice in one sentence: "Great, building a skill for `<task>`."
2. Propose a slash command name based on the task. Use kebab-case, short, descriptive. Examples:
   - "Reconciling Stripe payouts" → `/payout-reconcile`
   - "Pulling ad performance" → `/ad-pull`
   - "Weekly client recap" → `/client-recap`
3. Ask: "Is `<proposed-name>` good, or do you want a different name? Whatever you pick will be the slash command you type to run this skill."

Lock the name before continuing. This becomes `<slug>` for the produced skill.

---

## Phase 5: LIFECYCLE (Steps 1 to 3, in session)

The full lifecycle has six stages: identify, reverse-engineer, map, prove, retro, close the loop. You will walk the user through the first three in this session. The last three (prove, retro, close) happen automatically during normal use of the produced skill, thanks to the closed-loop hooks baked into every output.

### Step 5.1: Identify the core output

Ask:

> "When this skill finishes running successfully, what exists that didn't exist before? Be concrete. A specific file? A row added to a database? A Slack message posted? Describe the final artifact."

Capture in one or two sentences. If they describe a vague "report" or "update," push for the actual format: "Markdown file? Email? Discord message? Spreadsheet row?"

### Step 5.2: Reverse-engineer the path

Ask:

> "Starting from that finished output and working backwards: what's the last thing that has to happen right before that exists? And before that? And before that? Walk me backwards until you hit the starting point."

Capture each step as you go. You might end up with something like:

```
6. Final: a Markdown report saved to ~/Desktop/recap.md
5. ← Format the data into the report template
4. ← Pull the previous week's data from the source
3. ← Identify the date range for "last week"
2. ← Confirm which source to pull from
1. Starting point: the user types /<slug>
```

Don't worry yet about whether the steps are right. Just capture them.

### Step 5.3: Map the simplest path

Now flip the list forward. Walk the user through it in the natural order (step 1 to step N) and ask at each step:

1. "Is this step necessary?" If no, cut it.
2. "What does this step produce that the next step needs?" That's the checkpoint. Write it down.
3. "What could go wrong at this step?" Flag the failure mode. Surface it to the user during execution; don't let it pass silently.

After this pass you should have a numbered, trimmed list with a checkpoint per step. That IS the skill.

Confirm with the user: "Here's the path I'm about to bake into the skill. Look right?"

---

## Phase 6: BUILD

**Goal:** Write a complete, working SKILL.md and save the run history.

### Step 6.1: Compose the produced SKILL.md

Generate the file content using the template at the end of this document (see *Appendix: Produced-skill template*). Fill in:

- **Frontmatter `name`:** the slug from Phase 4
- **Frontmatter `description`:** one sentence, what the skill does and when to use it. Front-load the action and the trigger so it routes well.
- **What this skill does:** the core output from Step 5.1
- **When to use:** the trigger from the user's own words in Phase 1
- **Process:** the mapped path from Step 5.3, each step with its checkpoint and failure modes
- **Closed-loop hooks block:** verbatim from the template, do not modify

### Step 6.2: Write the file

Create the directory and write the file:

```bash
mkdir -p ~/.claude/skills/<slug>
```

Then write the composed content to `~/.claude/skills/<slug>/SKILL.md`.

Confirm to the user: "Wrote `~/.claude/skills/<slug>/SKILL.md`. You can invoke it right now as `/<slug>`."

### Step 6.3: Save the run history

Write a summary of this run to `~/.claude/skills/identify-skill/runs/<YYYY-MM-DD>_<slug>.md`:

```markdown
# /identify-skill run on <date>

## Candidates discovered
<the 5-10 candidate list>

## Scoring
<the ranking table>

## Picked
**Task:** <task>
**Skill name:** /<slug>

## Lifecycle answers (Steps 1-3)
1. **Core output:** <step 5.1>
2. **Reverse-engineered:** <step 5.2>
3. **Mapped path:** <step 5.3>

## Produced skill
`~/.claude/skills/<slug>/SKILL.md`

## Next steps
- Run /<slug> once on real work
- The skill will ask for feedback at the end (closed-loop hook), answer honestly
- Come back to /identify-skill in 1-2 weeks for the next opportunity
```

Create the `runs/` directory if it doesn't exist (`mkdir -p ~/.claude/skills/identify-skill/runs`).

### Step 6.4: Tell the user what happens next

Say something like:

> "Done. Two things to know:
>
> 1. Run `/<slug>` once on real work today or this week. It will ask you for feedback at the end and offer to update itself based on what you say. That's how Steps 4 through 6 of the lifecycle (prove, retro, close the loop) happen automatically.
> 2. Come back to /identify-skill in a week or two and we'll find the next thing."

---

## Closed-loop hook (self-applied to /identify-skill)

After Phase 6 is complete, before the session ends, ask the user:

> "Before you go: what was clunky about this interview itself? Any question that didn't land, any phase that felt slow or confusing, any beat I should add for next time?"

If they identify anything, propose specific edits to THIS file (`~/.claude/skills/identify-skill/SKILL.md`) and apply them with permission. The generator self-improves on every use, just like the skills it produces.

If they say "no, it was fine", accept that and end the session.

The first run of /identify-skill is the worst it will ever be. Iterate aggressively.

---

## Appendix: Produced-skill template

This is the template you fill in during Phase 6 and write to `~/.claude/skills/<slug>/SKILL.md`. Replace each `<placeholder>` with the captured content. Keep the closed-loop hooks block verbatim.

```markdown
---
name: <slug>
description: <one-sentence description, action + trigger>
---

# /<slug>

## What this skill does

<the core output, in one or two sentences from Step 5.1>

## When to use this

<the trigger, in the user's own words from Phase 1>

## Process

### Step 1: <name of step 1>

- **Do:** <what happens at this step>
- **Output (checkpoint):** <what this step produces that the next step needs>
- **Watch for:** <failure modes to surface to the user, not push past silently>

### Step 2: <name of step 2>

- **Do:** <what happens>
- **Output (checkpoint):** <what this produces>
- **Watch for:** <failure modes>

### Step N: <final step>

- **Do:** <what happens>
- **Output (checkpoint):** <the final core output>
- **Watch for:** <failure modes>

---

## Closed-loop hooks (do not remove)

After this skill produces its output, before ending the session:

1. Ask the user: "What broke, was confusing, or could be better about this run? Anything missing? Anything that felt slow?"
2. If the user identifies anything, propose specific edits to THIS file (`~/.claude/skills/<slug>/SKILL.md`) and apply them after confirmation.
3. If a step was unnecessary, cut it. If a step was missing, add it. If a checkpoint failed silently, add a check.
4. The first run of any skill is the worst it will ever produce with this system. Iterate aggressively.
```

---

## Tone notes (for Claude running this skill)

- Match the user's energy. If they're brief, be brief. If they brain-dump, write back in chunks.
- Don't lecture. The user came here for output, not a lesson.
- Don't apologize for asking questions. They are the work.
- If the user pushes back on a question or a tier, take their input. The formula is a starting point, not law.
- The user has finite time and energy. Every question must earn its place.
