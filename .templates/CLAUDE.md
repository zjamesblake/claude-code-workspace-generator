# {{YOUR_NAME}} — Workspace Map

{{DESCRIPTION}}

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

## Principles

- **Architecture over prompting.** The structure of your workspace determines the quality of every output. Build the workspace, not better prompts.
- **Living documentation.** Structural docs reflect current state at all times. If you change the territory, update the map. Outdated docs are worse than no docs.
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
