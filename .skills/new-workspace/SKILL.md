---
name: new-workspace
description: Add a new project or area of work to your existing workspace. Short interview, creates the folder with CONTEXT.md, and updates the root CLAUDE.md routing table. Use when starting a new project, onboarding a new client, or organizing a new area of work.
---

# /new-workspace

Add a new project or area of work through a short conversation. Creates the folder, writes the CONTEXT.md, and updates your root map so Claude knows where to find it.

## Usage

```
/new-workspace
/new-workspace client-delta
```

## When to Use

- Starting a new project or client
- Organizing existing work into a dedicated space
- Adding a new area of responsibility

---

## Process

### Phase 1: Interview (keep it short)

**Ask:**

**1. "What is this new workspace for?"**
Listen for: name, purpose, who it's for.

**2. "What tools or tech will you use here?"**
Listen for: platforms, apps, services.

**3. "What will you produce or deliver from here?"** (skip if obvious from #1)
Listen for: outputs, deliverables, recurring work.

**4. "Is there anything else I should know about how work happens here?"** (skip if simple)
Listen for: sub-areas, special rules, team members involved.

Stop early if the workspace is simple. Don't over-interview.

---

### Phase 2: Confirm the plan

Present what you'll create:

```
NEW WORKSPACE: {name}
━━━━━━━━━━��━━━━━━━━━━━━━━━

{workspace-name}/
├── CONTEXT.md                    ← Local guide for this area
├── {sub-area}/                   (if applicable)
└── {sub-area}/                   (if applicable)

Root CLAUDE.md updates:
  + Workspaces table: {name} | {description} | {tech}
  + Routing table: {task description} | {workspace-name}/ | CONTEXT.md
```

**Wait for approval before creating anything.**

---

### Phase 3: Create

1. Create the workspace folder
2. Create any sub-folders identified
3. Write CONTEXT.md for the workspace
4. Update root CLAUDE.md: add row to Workspaces table and Routing table

---

### Phase 4: Summary

```
WORKSPACE CREATED: {name}
━━━��━━━━━━━━━━━━━━━━━━━━━━

  {workspace-name}/CONTEXT.md           ✓
  Root CLAUDE.md updated                ✓

You can start working here now. If you have a repeating
process in this area, try /new-workflow to turn it into a skill.
```

---

## CONTEXT.md Format

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

{Any specific instructions or notes. Skip if simple.}
```

Only include sections that have content. Never create empty sections.

---

## Safety Rules

1. **Never overwrite existing files.** Check if the folder exists first.
2. **Always confirm before writing.** Show the plan and wait.
3. **Update the root map.** The CLAUDE.md routing table must reflect the new workspace.
4. **No secrets in generated files.**

---

## Edge Cases

### Folder already exists
Check what's inside. If CONTEXT.md exists, offer to update or skip. If files exist but no CONTEXT.md, document what's there.

### Very simple workspace (reference material, static files)
Skip questions 3-4. Create CONTEXT.md with header only. Still update root routing.

### User gives a name that doesn't match kebab-case
Convert it. "Client Delta" becomes `client-delta/`. Confirm with user.
