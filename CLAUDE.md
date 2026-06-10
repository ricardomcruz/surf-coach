# Surf Coach — Claude Code Context

This repository is a personalized surf coaching system powered by Claude agents and skills.

## Purpose

Help the user plan and improve their surfing by running structured agents and skills that analyse sessions, track goals, and provide coaching recommendations.

## Repository layout

- `agents/` — autonomous agents that run multi-step coaching workflows
- `skills/` — Claude Code skills for specific, reusable coaching tasks
- `data/sessions/` — surf session logs (JSON or Markdown)
- `data/goals/` — goals and milestones
- `data/profile/` — surfer profile (level, equipment, home break, objectives)
- `config/` — agent and skill configuration
- `docs/` — documentation

## Data conventions

### Session log (`data/sessions/YYYY-MM-DD.md`)
Each session is a Markdown file with: date, location, conditions (swell, wind, tide), board used, duration, what went well, what to improve, rating.

### Goal (`data/goals/goals.md`)
Goals follow the format: objective, current level, target level, deadline, actions.

### Profile (`data/profile/profile.md`)
Surfer profile: name, experience level, home break, boards, strengths, weaknesses, current focus.

## Conventions

- All data files are Markdown or JSON
- Session filenames: `YYYY-MM-DD.md`
- Agents are self-contained scripts in `agents/`
- Skills are Claude Code skill files in `skills/`
