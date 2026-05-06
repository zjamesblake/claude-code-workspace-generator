---
name: onboard
description: First-run skill that interviews the user about their work, then scaffolds a personalized workspace with CLAUDE.md, CONTEXT.md files, and visual folder maps. Designed for non-technical users with zero Claude Code experience.
---

# /onboard

Set up your workspace from scratch. This skill asks you about your work, figures out how to organize it, and creates the folder structure and documentation that makes Claude Code effective for you.

## Usage

```
/onboard
```

Run this once when you first start using Claude Code. It takes about 5 minutes.

---

## Process

### Phase 1: WELCOME

Start with a brief, warm introduction. 2-3 sentences. No jargon.

Say something like:

> I'm going to ask you about your work so I can set up a workspace that makes you faster. This takes about 5 minutes. I'll ask some questions, show you what I'd create, and build it once you approve.

Do not explain the architecture. Do not mention CLAUDE.md or CONTEXT.md yet. The user doesn't need to know the internals. They just need to answer questions about their work.

---

### Phase 2: UNDERSTAND THE PERSON

Ask these questions conversationally. Follow the natural flow. If one answer covers multiple questions, don't re-ask.

**1. "What do you do? What's your role?"**
Listen for: job title, industry, team size, whether they work alone or with others.

**2. "What tools and software do you use day to day?"**
Listen for: apps, platforms, services. This tells you what integrations matter later.

**3. "What are the main things you're responsible for producing or delivering?"**
Listen for: outputs, deliverables, recurring work. Reports, campaigns, content, operations, whatever they make.

**While listening, identify natural workspace boundaries.** Distinct areas of work become separate workspaces. Look for:
- Different tools or tech stacks
- Different clients or projects
- Different types of output
- Work that has nothing to do with other work

If something is unclear, ask a follow-up. Don't move on until you understand the shape of their work.

---

### Phase 3: MAP THE WORKSPACES

**Reflect back what you heard:**

> It sounds like you have [N] main areas of work: [list them]. Does that sound right?

Wait for confirmation. Let them correct you.

**Then for each workspace, ask:**

> Tell me a bit more about [area]. What do you actually do here?

Listen for:
- Sub-projects or modules within the area
- Specific tools used in that area
- What they produce or deliver
- Pain points or things that slow them down

**Keep it conversational.** If the user gives short answers, the workspace is simple. If they go deep, it's complex and needs more structure.

**Gauge complexity for each workspace:**
- **Simple** (reference material, single-tool work): CONTEXT.md only
- **Medium** (a few connected pieces, one or two integrations): CONTEXT.md with sub-routing
- **Complex** (multiple integrations, team handoffs): CONTEXT.md + detailed routing

---

### Phase 4: CONFIRM AND CREATE

#### 4a. Present the proposed structure

Show the full plan before creating anything. Use a visual folder map like this:

**The key principle: the root is YOU, not your job.** The root CLAUDE.md represents the person: their role, principles, preferences, how they work. Work areas (agency, side projects, personal) are folders underneath. This means if they change jobs, add side projects, or have personal areas, everything lives naturally under their identity.

```
YOUR WORKSPACE
━━━━━━━━━━━━━━━━━━━━━━━━━━

{name}-workspace/
├── CLAUDE.md                         ← YOU (always loaded)
│   "I am [name]. [Role/identity].
│    [How I work. My standards. My preferences.]
│    Routing: see folders below."
│
├── {work-area-1}/                    ← An area of your work
│   ├── CONTEXT.md                    ← Loaded when you're working here
│   ├── {sub-area}/
│   └── {sub-area}/
│
├── {work-area-2}/                    ← Another area (could be personal, side project, etc.)
│   ├── CONTEXT.md
│   └── {sub-area}/
    ├── CONTEXT.md                    �� [workspace-3] context (loaded when here)
    └── {sub-area}/
```

Explain briefly:
- "The CLAUDE.md at the top is YOU. It tells me who you are, how you work, and where everything lives. This is always loaded, no matter what you're working on."
- "Each folder is an area of your work or life. It has its own guide that tells me what happens there."
- "When you work in a specific area, I only load what's relevant. Everything else stays available but not active."
- "You can add areas anytime: more clients, personal projects, learning, whatever. It all lives under you."

**Wait for approval before creating anything.**

#### 4b. Create the workspace (in place)

**This folder becomes the workspace.** Do not create a new folder elsewhere.

**Order of operations:**

1. Create all sub-workspace folders inside the current directory
2. Write the root CLAUDE.md (personalized from template, replacing the generator CLAUDE.md)
3. Write CONTEXT.md for each workspace
4. Create any sub-folders identified in the interview
5. Clean up generator files: delete `.skills/`, `.templates/`, `README.md`, `system-docs/`

#### 4d. Present the completed structure

Show the visual map one more time with confirmation:

```
WORKSPACE READY
━━━━━━━━━━━━━━━━━━━━━━━━━━

  (this folder)
    CLAUDE.md                          ✓ You (always loaded)
    {work-area-1}/CONTEXT.md           ✓
    {work-area-2}/CONTEXT.md           ✓

What to do next:
  1. You're already in your workspace! Just start a new session.
  2. Try /new-workflow to turn one of your repeating processes into a skill
  3. Tip: you can rename this folder to something personal (like "zak-workspace")

Your workspace will grow as you use it. Every time you create
something new or change something, the maps update automatically.
```

---

## CLAUDE.md Format

Generate the root CLAUDE.md based on what you learned in the interview. Use the template in `.templates/CLAUDE.md` as the base and personalize it with:

- User's name or team name
- One-sentence description of what the workspace covers
- Populated Workspaces table (folder, description, tech)
- Populated Routing table (task description, folder, what to read)

Keep the Principles, File Classification, Skills, and "How This Works" sections from the template unchanged. They are universal.

---

## CONTEXT.md Format

Only include sections that have content. A simple workspace might just have the header and a few notes. A complex one gets sub-routing.

```markdown
# {Workspace Name}

{One paragraph: what it does, who it's for, why it exists.}

**Tools:** {technologies, platforms used here}

## What's Here

| Folder/File | What | Type |
|-------------|------|------|
| {sub-area}/ | {description} | Living |
| ... | ... | ... |

## How to Work Here

{Any specific instructions, standards, or notes about how work happens in this area. Skip if simple.}
```

---

## Safety Rules

1. **Never overwrite existing files.** Check first. If a file exists, ask before replacing.
2. **Always confirm before writing.** Show the plan (Phase 4a) and wait for explicit approval.
3. **Stay organized.** All workspace paths should use kebab-case for folders and snake_case.md for docs.
4. **No secrets in generated files.** Never create .env files or write credentials.
5. **Handle re-runs gracefully.** If the user runs /onboard again and some files exist, only create what's missing. Offer to update existing files.

---

## Tone and Style

- **Warm but efficient.** Friendly, brief. Not a chatbot personality exercise.
- **No jargon.** Don't say "scaffold," "architecture," or "context window." Say "set up," "structure," and "what I can see."
- **Don't over-explain.** The user doesn't need to know why the three-layer structure works. They just need their workspace set up.
- **Match their energy.** Short answers = keep it short. Detailed answers = engage.
- **Celebrate the finish.** When the workspace is created, make it feel like an accomplishment.

---

## Edge Cases

### User has only one area of work
That's fine. Create one workspace folder with CONTEXT.md and a root CLAUDE.md that routes to it.

### User isn't sure how to describe their work
Ask for examples. "What did you work on this week?" or "Walk me through a typical day."

### User wants to organize existing files
Document current state in CONTEXT.md, not aspirational state. Flag cleanup as a follow-up.

### User has very complex work (10+ areas)
Group related areas into parent workspaces. A marketing agency with 12 clients doesn't need 12 workspaces. They need a "clients" workspace with sub-routing per client, plus separate workspaces for internal ops.

### User runs /onboard in a folder that already has a CLAUDE.md
Check what exists. Offer to update the existing structure rather than replacing it.
