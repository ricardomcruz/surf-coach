# Surf Coach — Claude Code Context

This repository is a personalized surf coaching system powered by Claude skills. It acts as an intelligent personal surf coach — gathering data about the user, tracking sessions and goals, identifying patterns, and providing honest, tailored coaching.

## How to use

Always start with `/coach`. It reads the current state of the repo and guides the user from there.

## Available skills

| Skill | Command | Purpose |
|-------|---------|---------|
| Coach | `/coach` | Main entry point. Reads all data, acts as a personal coach, asks questions, spots patterns, suggests next actions. Always run this first. |
| Setup Profile | `/setup-profile` | Collects the user's surfing background and saves it to `data/profile/profile.md` |
| Setup Goals | `/setup-goals` | Defines or updates surf goals and saves them to `data/goals/goals.md` |
| Reset | `/reset` | Clears all user data and restores blank templates. Use when handing the repo to a new user. Skills are preserved. |

## Recommended first-run flow

1. `/coach` — the coach will detect no data and guide the user from here
2. `/setup-profile` — fill in the surfer profile
3. `/setup-goals` — set 1–3 concrete goals
4. Log your first session in `data/sessions/YYYY-MM-DD.md` (use `template.md` as base)
5. `/coach` — now the coach has context and can give real feedback

## Repository layout

```
surf-coach/
├── .claude/
│   └── skills/             # Claude Code skill definitions
│       ├── coach.md
│       ├── setup-profile.md
│       ├── setup-goals.md
│       └── reset.md
├── agents/                 # Future autonomous agents
├── skills/                 # Future standalone skill scripts
├── data/
│   ├── sessions/           # One .md file per surf session (YYYY-MM-DD.md)
│   ├── goals/goals.md      # User's active goals and milestones
│   └── profile/profile.md  # Surfer profile
├── config/config.json      # Configuration
└── docs/                   # Additional documentation
```

## Data conventions

### Session log (`data/sessions/YYYY-MM-DD.md`)
Use `data/sessions/template.md` as the base. One file per session. Include: location, conditions (swell, wind, tide), board, duration, what went well, what to improve, rating.

### Goals (`data/goals/goals.md`)
Max 3 active goals. Each goal must have: objective, current level, target, deadline, and concrete actions.

### Profile (`data/profile/profile.md`)
Surfer background: name, level, home break, boards, stance, strengths, weaknesses, current focus.

## Coaching philosophy

The coach reads ALL available data before responding. It doesn't give generic tips — it references the user's actual profile, goals, and session history. It identifies patterns across sessions, notices inconsistencies, and pushes the user when needed. It suggests running specific skills when relevant. It is honest, direct, and treats the user as a serious athlete.
