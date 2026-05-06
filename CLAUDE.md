# Claude Code Workspace Generator

This folder will become your workspace. When the user says "get started" (or anything indicating they want to begin setup), follow these instructions.

## Initialization Instructions

### Step 1: Install Skills

Copy the skills from this folder to the user's global skills directory. Run this command:

```bash
cp -r "$(pwd)/.skills/onboard" ~/.claude/skills/onboard && cp -r "$(pwd)/.skills/new-workspace" ~/.claude/skills/new-workspace && cp -r "$(pwd)/.skills/new-workflow" ~/.claude/skills/new-workflow && echo "Skills installed successfully."
```

Tell the user: "I'm installing three skills that will be available as commands in all your sessions. I just need your permission to copy some files."

After the command runs, confirm: "Skills installed. You now have /onboard, /new-workspace, and /new-workflow available."

### Step 2: Run Onboard (in place)

Immediately after skills are installed, begin the /onboard process. Read the skill at `.skills/onboard/SKILL.md` and follow its instructions to interview the user and scaffold their workspace.

**IMPORTANT: Build the workspace IN THIS FOLDER.** Do not create a new folder elsewhere. This folder transforms into their workspace. Create the sub-folders, write the CONTEXT.md files, and replace this CLAUDE.md with their personalized one.

### Step 3: Clean Up

After the workspace is scaffolded and the user has confirmed everything looks good:

1. Replace THIS CLAUDE.md with the personalized workspace CLAUDE.md (the one generated from the interview)
2. Delete the `.skills/` folder (skills are already installed globally)
3. Delete the `.templates/` folder (template has been used)
4. Delete `README.md` (no longer relevant, this is their workspace now)
5. Delete `system-docs/` folder (internal docs, not needed by the user)

The folder is now their workspace. Nothing left from the generator except the actual workspace files.

### Step 4: Suggest renaming (optional)

After cleanup, mention: "One last thing: you might want to rename this folder to something that makes sense for you (like your name or 'my-workspace'). You can do that in Finder. It won't break anything."

---

## If the user asks questions before starting

- **"What is this?"** — "This folder will become your AI workspace. It takes about 5 minutes to set up. I'll ask you some questions about your work, then organize this folder so Claude Code works much better for you. Type 'get started' when you're ready."
- **"Is this safe?"** — "This creates folders and text files inside this folder. That's all. It also copies three small skill files to your Claude Code settings. No system changes, no hidden installs."
- **"What if I mess up?"** — "Delete this folder and re-download it. 30 seconds. There's no risk."

---

## Important Notes

- Do NOT explain architecture, context windows, or technical concepts during setup.
- Do NOT mention CLAUDE.md or CONTEXT.md by name until Phase 4 of onboard (when showing the plan). Before that, say "your map" and "project guides."
- The workspace template is in `.templates/CLAUDE.md`. Personalize it during onboard.
- Keep the tone warm and efficient.
- **BUILD IN PLACE.** This folder becomes the workspace. Do not create a separate folder.
