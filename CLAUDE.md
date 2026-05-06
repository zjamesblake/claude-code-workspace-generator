# Claude Code Workspace Generator

This folder sets up your AI workspace. When the user says "get started" (or anything indicating they want to begin setup), follow these instructions.

## Initialization Instructions

### Step 1: Install Skills

Copy the skills from this folder to the user's global skills directory. Run this command:

```bash
cp -r "$(pwd)/.skills/onboard" ~/.claude/skills/onboard && cp -r "$(pwd)/.skills/new-workspace" ~/.claude/skills/new-workspace && cp -r "$(pwd)/.skills/new-workflow" ~/.claude/skills/new-workflow && echo "Skills installed successfully."
```

Tell the user: "I'm installing three skills that will be available as commands in all your sessions. I just need your permission to copy some files."

After the command runs, confirm: "Skills installed. You now have /onboard, /new-workspace, and /new-workflow available."

### Step 2: Run Onboard

Immediately after skills are installed, begin the /onboard process. Read the skill at `.skills/onboard/SKILL.md` and follow its instructions to interview the user and scaffold their workspace.

### Step 3: Clean Up

After the workspace is scaffolded and the user has confirmed everything looks good, replace the contents of THIS file (the CLAUDE.md in this generator folder) with:

```markdown
# Workspace Generator (Setup Complete)

Your workspace has been created. You can close this folder and open your new workspace in VS Code to start working.

**Your workspace location:** {path they chose}

**Skills installed:**
- /onboard — Re-run workspace setup
- /new-workspace — Add a new project or area
- /new-workflow — Turn a process into a reusable skill

**To get started in your new workspace:**
1. Open the workspace folder in VS Code
2. Open the Claude Code panel
3. Try /new-workflow to turn one of your processes into a skill

If you ever want to start fresh, delete your workspace folder and run this generator again.
```

This way the generator folder becomes a simple reference after use, and the user doesn't accidentally re-run setup.

---

## If the user asks questions before starting

- **"What is this?"** — "This sets up an AI workspace for you. It takes about 5 minutes. I'll ask you some questions about your work, then create a folder structure that makes Claude Code work much better for you. Type 'get started' when you're ready."
- **"Is this safe?"** — "This creates folders and text files. That's all it does. It copies three skill files to your Claude Code settings, and creates a workspace folder wherever you choose (Desktop by default). No system changes, no installations, nothing that affects the rest of your computer."
- **"What if I mess up?"** — "Delete the workspace folder and run this again. 30 seconds. There's no risk."

---

## Important Notes

- Do NOT explain architecture, context windows, or technical concepts during setup. The user just needs their workspace created.
- Do NOT mention CLAUDE.md or CONTEXT.md by name until Phase 4 of onboard (when showing the plan). Before that, say "your map" and "project guides."
- The workspace template is in `.templates/CLAUDE.md`. Personalize it during onboard.
- Keep the tone warm and efficient. This should feel easy, not technical.
