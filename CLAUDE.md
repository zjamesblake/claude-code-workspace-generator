# Claude Code Workspace Generator — Signpost

Workspace setup moved into the Team Build Kit. When the user says **"get started"** (or anything indicating they want to begin setup), follow these steps so they still end with a workspace.

## Step 1: Say where setup lives now

Tell the user: *"Workspace setup moved into the Team Build Kit, which carries this interview plus the standards and helpers a workspace needs. I'll install the kit's commands into your Claude Code now — it asks permission once — and then run the interview."*

## Step 2: Install the kit's commands

```bash
curl -fsSL https://raw.githubusercontent.com/zjamesblake/team-build-kit/main/install.sh | bash
```

Confirm the ✅ line and its file count. If it printed ❌, nothing was installed; say so and stop.

## Step 3: Run the interview

**Read the installed `~/.claude/skills/onboard/SKILL.md` and follow it.** It asks about the user's work in plain words, creates their workspace as a new folder (on the Desktop by default, since this folder is not the kit), installs the kit's workspace files into it, and writes their map and skills list. Do not build the workspace in this folder.

## Step 4: Point at the kit

After the interview's handoff card, say: *"Your workspace is ready. The kit's page has the rest — what the commands do and what to read first: https://github.com/zjamesblake/team-build-kit — and `/update-build-kit` keeps it current."*

---

## If the user asks questions before starting

- **"What is this?"** — "This used to be the setup folder. Setup now lives in the Team Build Kit; I can install it and run the interview from here in about ten minutes. Type 'get started' when you're ready."
- **"Is this safe?"** — "It copies skill files into your Claude Code settings and creates one new folder for your workspace. No system changes, no hidden installs."
- **"What if I mess up?"** — "Delete the workspace folder and run `/onboard` again. There's no risk."

## Important Notes

- Do NOT explain architecture, context windows, or technical concepts during setup.
- Keep the tone warm and efficient.
- `identify-skill/` stays in this repository; it is the companion to the CC-02 video and installs on its own.
