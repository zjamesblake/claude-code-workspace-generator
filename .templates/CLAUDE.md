# {{YOUR_NAME}}

{{DESCRIPTION}}

## About Me

{{ROLE_AND_CONTEXT}}

## Workspaces

| Folder | What | Tech |
|--------|------|------|
| _Fill in during onboard_ | | |

## Routing

| Task | Go to | Read first |
|------|-------|------------|
| _Fill in during onboard_ | | |
| New project or area of work | — | Use /new-workspace |

## Naming Conventions

| Type | Pattern | Example |
|------|---------|---------|
| Folders | kebab-case | client-work, content-ops |
| Docs | snake_case.md | meeting_notes.md |

## Rules

**When the territory changes, the maps must be updated.** Any time a folder is created, renamed, moved, or deleted, or any time routing, structure, or scope changes, the CLAUDE.md and any affected CONTEXT.md files must be updated in the same action. Never leave the maps out of sync with reality. This is not optional.

Claude maintains these maps. When you make a structural change, Claude will update the relevant documents automatically. You do not need to do this manually.

## Principles

- **Architecture over prompting.** The structure of your workspace determines the quality of every output. Build the workspace, not better prompts.
- **Right context at the right level.** Things always true about you go in the root CLAUDE.md. Things true about a project go in that project's CONTEXT.md. Things true about a specific workflow go in the skill. Never dump everything in one place.
- **Repeatability over one-shot.** When you do something twice, make it a skill. Every repeatable process should be a single command.
- **New mistakes only.** When something goes wrong, update the skill or context so it can never happen the same way again. The system gets smarter with every correction.

## File Classification

Not all files are the same. Know what you're creating:

| Type | What it is | Examples | Rule |
|------|-----------|----------|------|
| **Living** | Reflects current state. Must stay accurate. | CLAUDE.md, CONTEXT.md, routing tables | Update at the moment of change |
| **Static** | Records what was true at a point in time. Never needs updating. | Completed project archives, decision records | Create once, never modify |
| **Temporary** | Exists to serve a task. Delete when done. | Drafts, scratch notes, one-time scripts | Delete when the job is finished |

**Rule:** If you create a file, know which type it is. If you change something that a living document references, update that document immediately.

## Skills Available

| Skill | What it does | When to use |
|-------|-------------|-------------|
| /new-workspace | Add a new project or area of work | Starting something new |
| /new-workflow | Turn a repeating process into a reusable skill | You notice you do something regularly |
| /onboard | Re-run the workspace setup interview | Starting fresh or restructuring |

## How This Works

Your workspace uses a three-layer architecture:

```
CLAUDE.md        → The map (always loaded, routes to the right place)
CONTEXT.md       → The local guide (one per project, loaded when you're there)
Skills           → Specific workflows (loaded only when you invoke them)
```

This keeps Claude focused on what matters for your current task instead of loading everything into context. When you open a session in a specific folder, Claude reads the root map (this file) plus that folder's local guide. Everything else stays available but not active.
