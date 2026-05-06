# Architecture — Claude Code Workspace Generator

## What This Is

A downloadable folder that anyone can use to set up a structured AI workspace with Claude Code. No terminal commands, no git knowledge required. Open in VS Code, type "get started," answer questions, get a workspace.

## How It Works

```
User downloads zip from GitHub
    ↓
Unzips to Desktop, opens in VS Code
    ↓
Types "get started" in Claude Code panel
    ↓
Claude reads CLAUDE.md (initialization instructions)
    ↓
Copies .skills/* to ~/.claude/skills/ (one permission prompt)
    ↓
Runs /onboard interview
    ↓
Scaffolds personalized workspace at user's chosen location
    ↓
Rewrites generator CLAUDE.md to "setup complete" message
    ↓
User opens their new workspace and starts working
```

## Components

### .skills/ (staging area, copied to ~/.claude/skills/ during setup)

| Skill | Purpose | Category |
|-------|---------|----------|
| `/onboard` | First-run interview, scaffold workspace | Setup |
| `/new-workspace` | Add a new project area after initial setup | Growth |
| `/new-workflow` | Turn a repeating process into a reusable skill | Daily driver |

### .templates/

`CLAUDE.md` — the workspace template personalized during /onboard. Contains:
- Routing table (populated from interview)
- Principles (universal, baked in)
- File Classification guide (living vs. static vs. temporary)
- Skills reference
- "How This Works" section explaining the three layers

### Root CLAUDE.md

Contains initialization instructions. When user says "get started":
1. Install skills (copy command)
2. Run /onboard
3. Rewrite itself to "setup complete"

After use, this file becomes a simple reference pointing to the user's workspace.

## Design Decisions

### Why "type get started" instead of a script
Non-technical users don't know how to run bash scripts. They DO know how to type a message to Claude. Meeting them where they are.

### Why skills are global, not per-workspace
Skills live in `~/.claude/skills/` (global) rather than in the workspace:
- Same skills work across all workspaces
- Skills update independently of workspace content
- User's work is never touched by skill updates

### Why interview-based, not template-based
A static template scaffolds the same structure for everyone. The interview adapts to actual complexity. A media buyer gets a different structure than a content creator. The principles are constant; the shape is personal.

### Why dot-prefix on .skills/ and .templates/
Keeps them visually hidden from the user. They don't need to interact with these files. Claude can still read them fine.

### Why the generator folder rewrites its own CLAUDE.md
Prevents accidental re-runs. After setup, the generator folder is "spent." The user works in their new workspace, not here.

### Why only 3 skills (not 7)
Original version shipped with /build, /audit, /close-project, /quick-fix. These are power-user tools that overwhelm beginners. Starter pack is: set up, grow, and build your first skill. Advanced skills available as a separate download later.

## Principles (embedded in all skills and the workspace template)

- **Three-layer architecture:** CLAUDE.md (map) > CONTEXT.md (local guide) > Skills (workflows). Context delivery, not file organization.
- **Locality:** Load only what's relevant. Projects are siloed.
- **Living documents:** Structural docs reflect current state. Territory changes = map updates.
- **Right context at the right level:** Root = always true. Project = true here. Skill = true for this workflow.
- **Repeatability:** Do it twice, make it a skill.
- **New mistakes only:** Every correction becomes permanent. System gets smarter.
- **File classification:** Every file is living, static, or temporary. Know which before creating.

## Update Strategy

Users re-download the generator zip to get updated skills. They can copy the new `.skills/` contents to `~/.claude/skills/` manually, or re-run the setup process (it handles existing files gracefully).
