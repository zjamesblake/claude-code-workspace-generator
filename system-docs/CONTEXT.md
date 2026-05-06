# System Documentation — Workspace Generator

Internal documentation for how this repo works. For Zak's reference only; users don't see this.

## Contents

| Document | Purpose |
|----------|---------|
| architecture.md | How the system works, components, design decisions |
| change_log.md | What changed, when, why |

## How to Work Here

- Modifying a skill: edit in `.skills/{skill-name}/SKILL.md`
- Adding a new skill: create folder in `.skills/`, update CLAUDE.md copy command, update architecture.md
- Updating the template: edit `.templates/CLAUDE.md`
- After any change: update architecture.md if structure changed
