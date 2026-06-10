# Surf Coach — Claude Code Context

This repository is a personalized AI surf coaching system. It acts as an intelligent personal surf coach — gathering athlete data, tracking sessions and goals, identifying patterns, and providing honest, tailored coaching through a set of skills.

---

## Core rule: private vs everything else

The only special folder is `private/`. Everything outside of it is part of the coaching system and is safe to share.

### `private/`
Contains **everything specific to the athlete**. This folder is gitignored and stays local. Never move athlete data outside of `private/`. Never reference `private/` paths from agents or skills at the root level.

- `private/data/sessions/` — session logs (one `.md` file per session)
- `private/data/goals/goals.md` — goals and milestones
- `private/data/profile/profile.md` — surfer profile
- `private/agents/` — athlete-specific agents (not shared)
- `private/skills/` — athlete-specific skills (not shared)

### Everything else
All other files and folders — `.claude/`, `agents/`, `config/`, `docs/`, `README.md`, `CLAUDE.md` — are part of the shared coaching system and contain no athlete data.

---

## Available skills

| Command | Purpose |
|---------|---------|
| `/coach` | **Start here.** Reads all athlete data and acts as a personal coach. Detects missing data, spots patterns, asks questions, suggests actions. |
| `/setup-profile` | Conversational intake to fill in `private/data/profile/profile.md` |
| `/setup-goals` | Goal-setting session. Saves up to 3 active goals to `private/data/goals/goals.md` |
| `/setup-metrics` | Collects health and performance metrics (HRV, sleep, VO2 max, body composition, posture, etc.). Saves to `private/data/metrics/metrics.md` |
| `/setup-activities` | Collects and evaluates out-of-water training activities (gym, yoga, swimming, skate, etc.) including availability per activity. Saves to `private/data/activities.md` |
| `/plan-gym` | Creates a structured gym programme with 3 session types: A (Strength/Power), B (Functional/Surf-Specific), C (Active Recovery). The weekly planner assigns the right type based on surf schedule and recovery state. Saves to `private/data/gym-programme.md` |
| `/setup-nutrition` | Collects the athlete's nutritional profile: restrictions, preferences, cooking capacity, goals, shopping habits. Saves to `private/data/nutrition-profile.md` |
| `/plan-week` | Plans the full training week. Fetches surf forecast, maps availability, assigns gym session types, generates meal plan per day adapted to training load, and produces a shopping list. Saves to `private/data/plans/YYYY-WNN.md` |
| `/log-session` | Debrief after surfing. Captures session details + pre-session metric snapshot. Saves to `private/data/sessions/YYYY-MM-DD.md` |
| `/evolve` | Meta-skill. Audits the full ecosystem, identifies gaps, proposes and implements improvements — new skills, agents, coach upgrades, integrations. Run every 4–8 weeks or when the athlete hits a plateau or major milestone. |
| `/reset` | Clears all athlete data in `private/`. Preserves the full coaching system. Resets for a new user. |

## Recommended first-run flow

1. `/coach` — detects no data, guides the athlete from here
2. `/setup-profile` — fill in the surfer profile
3. `/setup-goals` — set 1–3 concrete goals
4. `/setup-metrics` — capture health and performance baselines
5. `/setup-activities` — log available out-of-water training and availability slots
6. `/plan-gym` — create the gym programme (session types A/B/C)
7. `/setup-nutrition` — set up nutritional profile and preferences
8. `/plan-week` — plan the first training week (includes meal plan + shopping list)
7. Go surf → `/log-session` → repeat
8. `/coach` regularly — the more data, the better the coaching

---

## Data conventions

### Session log — `private/data/sessions/YYYY-MM-DD.md`
One file per session. Use `template.md` as base. Must include: location, conditions, board, duration, what went well, what to improve, goal check, ratings, and coach's note.

### Goals — `private/data/goals/goals.md`
Max 3 active goals. Each must have: objective, current level, target, deadline, and concrete actions.

### Profile — `private/data/profile/profile.md`
Surfer background: name, level, home break, boards, stance, strengths, weaknesses, current focus.

### Metrics — `private/data/metrics/metrics.md`
Health and performance baselines: HRV, resting heart rate, sleep, VO2 max, body composition, posture, stress, energy, motivation. Updated via `/setup-metrics`. A snapshot of the most relevant fields is also captured in each session log under "Pre-session state".

### Activities — `private/data/activities.md`
Out-of-water training available to the athlete: what they do, when they can do it (fixed slots vs flexible), and coach's assessment. Used by `/plan-week` to schedule complementary training within real availability constraints.

### Gym programme — `private/data/gym-programme.md`
Structured gym programme with 3 session types: A (Strength/Power), B (Functional/Surf-Specific), C (Active Recovery). Full exercises, sets, reps, and cues. `/plan-week` assigns the right type to each gym slot based on surf schedule and recovery state.

### Nutrition profile — `private/data/nutrition-profile.md`
Athlete's nutritional context: restrictions, allergies, dietary choices, goals, cooking capacity, shopping habits, and food preferences. Used by `/plan-week` to generate daily meal suggestions and a weekly shopping list.

### Evolution log — `private/data/evolution-log.md`
Log of every `/evolve` run: what was proposed, what was implemented, what was deferred and why. Gives future `/evolve` runs memory of past decisions.

### Weekly plans — `private/data/plans/YYYY-WNN.md`
One file per week (e.g. `2025-W23.md`). Contains forecast summary, surf session targets, day-by-day schedule, and coaching notes. Generated by `/plan-week`.

---

## Coaching philosophy

Every skill reads the athlete's actual data before responding — no generic advice. The coach identifies patterns across sessions, notices goal misalignment, and pushes the athlete when needed. It suggests other skills when relevant. It treats the athlete as a serious person working towards real objectives.

---

## Reset behaviour

Running `/reset` clears everything in `private/` (data, private agents, private skills) and restores blank templates. All other files are preserved and immediately usable by a new athlete.
