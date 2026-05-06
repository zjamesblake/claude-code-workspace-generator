# Claude Code Workspace Generator

Set up a structured AI workspace in 5 minutes. No coding required.

## What This Does

Creates a personalized workspace that organizes your work so Claude Code always knows what you're doing and what context to load. After setup, you'll have:

- A workspace map that routes Claude to the right context for any task
- Skills to create new projects and turn your processes into reusable commands
- A structure that gets smarter as you use it

## Quick Start

### 1. Download

Download this folder from GitHub (Code > Download ZIP). Unzip it. Put it on your Desktop.

### 2. Open in VS Code

Open VS Code. Go to File > Open Folder. Select this folder.

### 3. Open Claude Code

Open the Claude Code panel (click the Claude icon in the sidebar, or use the keyboard shortcut).

### 4. Type "get started"

Claude will:
- Install your skills (asks permission once to copy files)
- Ask you about your work (5 minute conversation)
- Transform this folder into your personalized workspace

That's it. This folder IS your workspace now. You're already in it. Start working.

## Skills Included

| Skill | What it does |
|-------|-------------|
| `/onboard` | First-run setup: interview + workspace creation |
| `/new-workspace` | Add a new project or area of work |
| `/new-workflow` | Turn a repeating process into a one-command skill |

## How It Works

Your workspace uses three layers:

```
CLAUDE.md        → The map (always loaded, tells Claude where everything is)
CONTEXT.md       → Local guides (one per project, loaded when you're there)
Skills           → Workflows (loaded only when you invoke them)
```

Claude only loads what's relevant to your current task. This keeps it focused and prevents the "context overload" problem you've probably hit in the browser.

## FAQ

**Is this safe?**
It creates folders and text files. That's all. No system changes, no hidden installs.

**What if I mess up?**
Delete the workspace folder. Run the generator again. 30 seconds.

**Do I need to know how to code?**
No. Everything is in plain English. You edit text files.

**Can I use this for multiple projects?**
Yes. Use `/new-workspace` to add projects anytime.

## Credits

Built by Zachary Blake. Architecture principles from Jake Van Clief.
