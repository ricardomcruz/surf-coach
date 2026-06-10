---
name: reset
description: Resets the repository to a clean state — removes all athlete data (profile, goals, sessions, private agents and skills) while preserving the full surf coach structure. Use this when handing the project to a new user.
---

You are about to reset the surf-coach repository to a clean state for a new user.

## Before doing anything

Warn the user clearly:

> "This will permanently delete all your profile, goals, session logs, and any private agents or skills. The full surf coach structure — all shared skills, agents, and config — will be preserved and ready for a new athlete. This cannot be undone. Are you sure?"

Wait for explicit confirmation ("yes", "proceed", "do it"). If they say anything else or seem unsure, stop and do nothing.

## What to reset (inside `private/`)

Once confirmed:

1. **Profile** — Overwrite `private/data/profile/profile.md` with the blank template
2. **Goals** — Overwrite `private/data/goals/goals.md` with the blank template
3. **Sessions** — Delete all `.md` files inside `private/data/sessions/` except `template.md`
4. **Private agents** — Delete all files inside `private/agents/` except `.gitkeep`
5. **Private skills** — Delete all files inside `private/skills/` except `.gitkeep`

## What to preserve (never touch)

- Everything in `shared/` — all shared agents and skills
- Everything in `.claude/` — all skill definitions
- `private/data/sessions/template.md`
- `config/config.json`
- `README.md`, `CLAUDE.md`, `.gitignore`

## After resetting

Tell the user clearly what was deleted. Then say:

> "The repo is clean and ready for a new athlete. To get started, run `/coach` — it will guide you from there."

## Blank profile template

```markdown
# Surfer Profile

## Personal
- **Name:**
- **Age:**
- **Location / Home break:**
- **Years surfing:**
- **Current level:** (Beginner / Intermediate / Advanced / Expert)

## Equipment
- **Boards:**
- **Wetsuit:**

## Surfing
- **Stance:** (Regular / Goofy)
- **Strengths:**
- **Weaknesses / areas to improve:**
- **Current focus:**

## Favourite breaks
-

## Notes
-
```

## Blank goals template

```markdown
# Surf Goals

## Active Goals

### Goal 1
- **Objective:**
- **Current level:**
- **Target:**
- **Deadline:**
- **Actions / drills:**
- **Progress:**

---

## Completed Goals

(Move goals here once achieved)

---

## Milestones

| Milestone | Target date | Status |
|-----------|-------------|--------|
|           |             |        |
```
