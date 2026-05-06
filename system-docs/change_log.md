# Changelog — Claude Code Workspace Generator

## [0.2.0] - 2026-05-06 - Non-Technical Rebuild

### Changed
- Complete restructure for non-technical audience (CC-01 viewers)
- Install process: "download folder, open in VS Code, type get started" (was: git clone + bash script)
- Skills moved to `.skills/` staging directory (dot-prefix, hidden from users)
- Template moved to `.templates/` (dot-prefix, hidden from users)
- CLAUDE.md now contains initialization instructions (handles full setup flow)
- Generator self-cleans after use (rewrites CLAUDE.md to "setup complete")
- README rewritten for non-technical users (no terminal commands)

### Added
- `/new-workflow` skill (reimagined from identify-workflow). Daily driver for building skill library.
- File Classification section in workspace template (living vs. static vs. temporary)
- "New mistakes only" principle in workspace template
- "How This Works" section explaining three-layer architecture

### Removed
- `install.sh` (replaced by Claude copying files on "get started")
- `/build`, `/quick-fix`, `/audit`, `/close-project` (moved to advanced pack)
- Old `skills/` directory (replaced by `.skills/`)
- Old `workspace-template/` directory (replaced by `.templates/`)

### Why
Audience shifted from power users to non-technical team members. Setup needed to be zero-friction.

---

## [0.1.0] - 2026-04-08 - Initial Build

### Added
- Initial repo with 7 skills, workspace template, and install script.
- Skills: /onboard, /new-workspace, /build, /quick-fix, /identify-workflow, /audit, /close-project
- Template: CLAUDE.md with build principles, lifecycle, living documentation rule
