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

## Specialist agent team

The coaching system uses a multi-agent architecture. The `/coach` skill acts as the orchestrating head coach. Before each session it consults a team of specialist agents, collects their assessments, and synthesises them into a coherent coaching picture. The athlete always speaks with the surf coach — the specialists work in the background.

Specialist agents live in `.claude/agents/`:

| Agent | File | Domain |
|-------|------|--------|
| Psychologist | `.claude/agents/psychologist.md` | Mental performance, stress, motivation, life-surf balance, wellbeing |
| Mobility Coach | `.claude/agents/mobility-coach.md` | Posture, movement quality, yoga, technique blockers with a physical root cause |
| Nutritionist | `.claude/agents/nutritionist.md` | Sports nutrition, body recomposition, anti-inflammatory diet, recovery nutrition |
| Gym Coach | `.claude/agents/gym-coach.md` | Strength & conditioning, surf-specific programming, training load, periodisation |
| Chinese Medicine Doctor | `.claude/agents/chinese-medicine-doctor.md` | TCM patterns, energetic balance, Qi dynamics, systemic prevention, seasonal rhythms |
| Physiotherapist | `.claude/agents/physiotherapist.md` | Injury prevention, prehab, musculoskeletal risk, tissue loading under surf-specific load |
| Surf Technique Coach | `.claude/agents/surf-technique-coach.md` | Surf technique analysis, manoeuvre biomechanics, drill prescription, progression tracking |
| Breathing Coach | `.claude/agents/breathing-coach.md` | Functional breathing, CO2 tolerance, hold-down preparation, nervous system via breath |
| Sleep Specialist | `.claude/agents/sleep-specialist.md` | Sleep science, chronobiology, sleep architecture, recovery optimisation |
| Psychosomatic Doctor | `.claude/agents/psychosomatic-doctor.md` | Mind-body patterns, somatic symptom expression, BFRB, psychosomatic medicine |
| Spiritual Guide | `.claude/agents/spiritual-guide.md` | Presence, contemplative practice, ocean relationship, meaning, non-doing |
| Periodisation Coach | `.claude/agents/periodisation-coach.md` | Long-term training arc, mesocycles, seasonal swell window planning, peak/taper timing |
| Life Coach | `.claude/agents/life-coach.md` | Habit formation and elimination, daily routine design, behavioural change, Atomic Habits framework |
| Health Coach | `.claude/agents/health-coach.md` | Biohacking, supplementation, longevity strategies, HRV optimisation, exogenous hormesis (cold/heat), systemic inflammation, biomarkers |

**Orchestration logic:** The coach always has `psychologist` + `mobility-coach` assessments available (from cache or fresh). For most sessions, `surf-technique-coach` is added if a session was recently logged. Additional specialists are invoked based on session relevance — never all 14 at once. The freshness gate prevents redundant re-invocations when no new data exists. The coach synthesises all input before opening the session.

**Cross-specialist reading:** Each specialist reads selected peer reports (`latest.md` from previous sessions) before writing their own assessment. This creates cross-domain awareness without ordering conflicts — specialists run in parallel but use the previous session's peer reports as context. The dependency map (who reads whom) is defined within each agent file under "Cross-specialist context". The coach still performs final synthesis — specialists don't negotiate directly.

**Specialist reports:** Each specialist writes a compact `latest.md` (≤25 lines) for the coach to read quickly, and archives the full assessment to `archive/YYYY-MM-DD.md`. Reports live in `private/data/specialist-reports/[name]/`.

**Adding new specialists:** Create a new `.md` file in `.claude/agents/` with `name`, `description`, and specialist instructions. Update the specialist roster table in `.claude/skills/coach.md` and `.claude/commands/coach.md`.

---

## Production agents

Three additional agents handle the generation and continuous improvement of the weekly plan HTML page. They are invoked by `/plan-week` after the plan content is written, not by `/coach`.

| Agent | File | Role |
|-------|------|------|
| Product Designer | `.claude/agents/product-designer.md` | Designs the visual layout, information architecture, and component spec for the weekly HTML page. Invoked once to create `private/data/plans/template-spec.md`, and again each week after the reviewer's feedback to update it. |
| HTML Engineer | `.claude/agents/html-engineer.md` | Reads the markdown plan + template spec and generates a complete self-contained `private/data/plans/YYYY-WNN.html` file. Invoked every time `/plan-week` runs. |
| Plan-Week Reviewer | `.claude/agents/plan-week-reviewer.md` | UX and product design reviewer. Invoked after html-engineer generates the page. Reads the HTML from the athlete's real use-case perspective (phone before surf, at the gym, at the supermarket). Writes a structured design feedback report to `private/data/plans/design-feedback.md`, then invokes the product-designer to update the template spec for the next iteration. |

**Workflow:** `/plan-week` saves the markdown plan → invokes `html-engineer` → HTML page generated → athlete approves plan → `plan-week-reviewer` runs in background → writes `design-feedback.md` → invokes `product-designer` → `template-spec.md` updated → next week's html-engineer picks up the improved spec.

**Self-improving loop:** Every `/plan-week` run produces a better page than the last. The reviewer identifies what isn't working, the product-designer updates the spec, and the engineer implements it — without any manual intervention from the athlete.

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
| `/log-session` | Debrief after surfing. Captures session details + pre-session metric snapshot. Cross-references conditions with Stormglass data. Captures video-coaching feedback if applicable. Saves to `private/data/sessions/YYYY-MM-DD.md` |
| `/log-gym` | Debrief after a gym session. Reads actual workout from Hevy if available, captures subjective state and niggles. Flags arm/shoulder fatigue if surf training is planned within 24h. Saves to `private/data/sessions/YYYY-MM-DD-gym.md` |
| `/consult [topic]` | Multidisciplinary consultation. Invokes 3–4 specialists **sequentially** on a specific topic — each reads what the previous ones wrote before contributing. Produces layered, non-contradictory reasoning. Use when a problem has clear roots in multiple domains simultaneously. Topics: recovery, technique, mental health, physical health, habits, periodisation. |
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

### Metrics — `private/data/metrics/YYYY-MM-DD/`
One dated folder per metrics update (e.g. `private/data/metrics/2026-06-10/`). Each folder contains:
- `metrics.md` — full snapshot: HRV, resting heart rate, sleep, VO2 max, body composition, posture, stress, energy, motivation, coach's read
- `front.jpg`, `back.jpg`, `side.jpg` — optional reference photos for postural and conditioning tracking

Agents and skills always list the directory and read the **most recent dated folder**. Never overwrite a previous entry — each folder is a permanent record.

`private/data/metrics/body-measurements.md` — summary table at the root level, one row per entry, auto-updated by `/setup-metrics`. Used for quick comparison across dates without opening individual folders.

Updated via `/setup-metrics`. A snapshot of the most relevant fields is also captured in each session log under "Pre-session state".

### Activities — `private/data/activities.md`
Out-of-water training available to the athlete: what they do, when they can do it (fixed slots vs flexible), and coach's assessment. Used by `/plan-week` to schedule complementary training within real availability constraints.

### Gym programme — `private/data/gym-programme.md`
Structured gym programme with 3 session types: A (Strength/Power), B (Functional/Surf-Specific), C (Active Recovery = mobility day). Full exercises, sets, reps, and cues. `/plan-week` assigns the right type to each gym slot based on surf schedule and recovery state.

### Yoga programme — `private/data/yoga-programme.md`
Structured yoga programme — the **D** session type. Self-guided flows (D1 thoracic/shoulder opening, D2 hips/posterior chain, D3 evening restorative), each with safety-brake cues built around the athlete's confirmed postural findings. Authored by the `mobility-coach`. `/plan-week` assigns the right flow per day.

### Qigong programme — `private/data/qigong-programme.md`
Structured qigong programme — the **E** session type. Short routines (E1 morning activation, E2 evening down-regulation, E3 thoracic), rooted in the athlete's TCM pattern. Authored by the `chinese-medicine-doctor`. E2 is the high-leverage evening routine for sleep; E2 and D3 are alternatives for the same evening slot.

### Land surf-training — `private/data/land-surf-training.md`
Land-based surf-skill programme ("power surfing" logic) — recreates surf phases/manoeuvres on land. 5 blocks (pop-up, bottom turn, cutback backside, slackline, surfskate), each tied to an active technique goal and the latest frame analysis. Authored by the `surf-technique-coach`. Block 1 is daily; slackline (Block 4) is a fixed weekly fixture; surfskate (Block 5) is the longer transfer session.

### Nutrition profile — `private/data/nutrition-profile.md`
Athlete's nutritional context: restrictions, allergies, dietary choices, goals, cooking capacity, shopping habits, and food preferences. Used by `/plan-week` to generate daily meal suggestions and a weekly shopping list.

### Evolution log — `private/data/evolution-log.md`
Log of every `/evolve` run: what was proposed, what was implemented, what was deferred and why. Gives future `/evolve` runs memory of past decisions.

### Weekly plans — `private/data/plans/YYYY-WNN.md`
One file per week (e.g. `2025-W23.md`). Contains forecast summary, surf session targets, day-by-day schedule, and coaching notes. Generated by `/plan-week`.

---

## External integrations (MCP)

Three MCP integrations are configured to reduce friction and improve data quality. All are optional — skills degrade gracefully if the MCP is unavailable.

### Hevy (gym workouts)
- **Config:** `.claude/settings.local.json` → `mcpServers.hevy`
- **Requires:** Hevy PRO subscription + API key (set `HEVY_API_KEY` in settings.local.json)
- **Setup:** Get your API key at app.hevyapp.com → Settings → API. Replace the placeholder in settings.local.json.
- **Used by:** `gym-coach` agent — reads actual workout data (exercises, sets, reps, loads) instead of only the planned programme
- **Tools available:** `mcp__hevy__list_workouts`, `mcp__hevy__get_workout`, `mcp__hevy__list_routines`

### Open-Meteo Marine API (surf forecast)
- **Config:** WebFetch permission — `marine-api.open-meteo.com` and `api.open-meteo.com` (already whitelisted)
- **Requires:** Nothing — free API, no key needed
- **Used by:** `plan-week` skill — fetches structured wave height, period, direction and wind data per spot using GPS coordinates from `surf-spots.md`
- **Fallback:** `pt.surf-forecast.com` via WebFetch if API call fails

### Apple Health (HRV, sleep, resting HR)
- **Config:** `.claude/settings.json` → `mcpServers.apple-health`
- **Requires:** Apple Health export. On iPhone: Settings → [name] → Health → Export Health Data → AirDrop or share to Mac → unzip to `~/Downloads/apple_health_export/`
- **Setup:** Export once, repeat monthly or when metrics feel stale. The MCP reads from `~/Downloads/apple_health_export/export.xml`.
- **Used by:** `setup-metrics` skill — pre-fills HRV, sleep, and resting HR from Apple Watch data before the conversation
- **Note:** If the export path is different, update `args` in `.claude/settings.json`

---

## Coaching philosophy

Every skill reads the athlete's actual data before responding — no generic advice. The coach identifies patterns across sessions, notices goal misalignment, and pushes the athlete when needed. It suggests other skills when relevant. It treats the athlete as a serious person working towards real objectives.

---

## Reset behaviour

Running `/reset` clears everything in `private/` (data, private agents, private skills) and restores blank templates. All other files are preserved and immediately usable by a new athlete.
