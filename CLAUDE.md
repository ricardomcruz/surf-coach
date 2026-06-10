# Surf Coach — Claude Code Context

This repository is a personalized AI surf coaching system. It acts as an intelligent personal surf coach — gathering athlete data, tracking sessions and goals, identifying patterns, and providing honest, tailored coaching through a set of skills.

---

## Core rule: shared vs private

The project is split into two root-level directories. This separation is fundamental and must always be respected:

### `shared/`
Contains everything that is **athlete-agnostic** — skills and agents that implement coaching logic but never store, reference, or expose any personal athlete data. This folder is safe to share publicly or reuse across athletes.

- `shared/agents/` — autonomous coaching agents (athlete-agnostic)
- `shared/skills/` — standalone skill scripts (athlete-agnostic)

**Rule:** Nothing in `shared/` may read from or write to `private/`. All data paths must be passed in as arguments or configuration.

### `private/`
Contains **everything specific to the athlete**. This folder is gitignored and stays local. It includes:

- `private/data/sessions/` — session logs (one `.md` file per session)
- `private/data/goals/goals.md` — goals and milestones
- `private/data/profile/profile.md` — surfer profile
- `private/agents/` — athlete-specific agents (not shared)
- `private/skills/` — athlete-specific skills (not shared)

**Rule:** Never move athlete data out of `private/`. Never reference `private/` paths from anything in `shared/`.

---

## Available skills

| Command | Purpose |
|---------|---------|
| `/coach` | **Start here.** Reads all athlete data and acts as a personal coach. Detects missing data, spots patterns, asks questions, suggests actions. |
| `/setup-profile` | Conversational intake to fill in `private/data/profile/profile.md` |
| `/setup-goals` | Goal-setting session. Saves up to 3 active goals to `private/data/goals/goals.md` |
| `/log-session` | Debrief after surfing. Saves a session log to `private/data/sessions/YYYY-MM-DD.md` |
| `/reset` | Clears all athlete data in `private/`. Preserves all shared structure. Resets for a new user. |

## Recommended first-run flow

1. `/coach` — detects no data, guides the athlete from here
2. `/setup-profile` — fill in the surfer profile
3. `/setup-goals` — set 1–3 concrete goals
4. Go surf → `/log-session` → repeat
5. `/coach` regularly — the more data, the better the coaching

---

## Data conventions

### Session log — `private/data/sessions/YYYY-MM-DD.md`
One file per session. Use `template.md` as base. Must include: location, conditions, board, duration, what went well, what to improve, goal check, ratings, and coach's note.

### Goals — `private/data/goals/goals.md`
Max 3 active goals. Each must have: objective, current level, target, deadline, and concrete actions.

### Profile — `private/data/profile/profile.md`
Surfer background: name, level, home break, boards, stance, strengths, weaknesses, current focus.

---

## Coaching philosophy

Every skill reads the athlete's actual data before responding — no generic advice. The coach identifies patterns across sessions, notices goal misalignment, and pushes the athlete when needed. It suggests other skills when relevant. It treats the athlete as a serious person working towards real objectives.

---

## Reset behaviour

Running `/reset` clears everything in `private/` (data, private agents, private skills) and restores blank templates. The full `shared/` structure and all `.claude/skills/` definitions are preserved and immediately usable by a new athlete.
