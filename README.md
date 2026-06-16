# Surf Coach

A personal coaching system for surfers, built on Claude Code. It works like having a coaching team available anytime — one that knows you, remembers everything, and gets more precise the more you use it.

---

## What is this

Imagine having access to a personal surf coach plus a team of 14 background specialists: psychologist, physiotherapist, nutritionist, sleep specialist, mobility coach, gym coach, surf technique coach, health coach, breathing coach, Chinese medicine doctor, periodization coach, life coach, psychosomatic doctor, and spiritual guide.

You don't talk to all of them directly. Your surf coach reads their assessments before each session and uses that context to give you integrated coaching — like a GP consulting specialists before your appointment.

The system learns with you. The more sessions you log, the more precise it becomes. A coach with 3 sessions of data is useful. A coach with 30 sessions, metrics, goals, and a structured gym program is something else entirely.

---

## What this is not

**It doesn't replace real professionals.** When something needs a blood test, hands-on physiotherapy, or clinical evaluation, the system tells you that directly and points you toward help. That handoff is part of how it works, not a limitation.

**It's not a shortcut.** It works in proportion to what you give it. Honest, regular logs create real coaching. Superficial use yields superficial results.

**It's not infallible.** It works with what you report. You're the source of truth — the system is your thinking partner, not your authority.

---

## What makes it different

**Memory that doesn't fade.** Every session, every metric, every observation stays available forever. You never have to re-explain your history. The coach picks up exactly where it left off.

**A team that communicates.** Specialists read each other's reports before writing their own. The physiotherapist knows what the gym coach prescribed. The health coach knows what the sleep specialist found. This level of integration doesn't exist in real human teams.

**Always available.** At 11pm before a surf trip. On a rest day when you want to think through your goals. Right after getting out of the water while the session is still fresh.

**Honest, not motivational.** The coach tells you when you're avoiding your main goal, when your session frequency doesn't match your ambitions, and when what you planned and what you did aren't the same thing.

---

## Honest trade-offs

| What AI coaching does well | What a human coach does better |
|---|---|
| Perfect memory of every session | Reading your body language and energy |
| Integrated team that communicates | Direct physical observation and hands-on assessment |
| Always available, no scheduling | Real accountability through relationship |
| No ego or hidden agenda | Intuitive pattern recognition over years |
| Dramatically lower cost | The therapeutic effect of human connection |

---

## Prerequisites

- [Claude Code](https://claude.ai/code) installed
- Claude Pro subscription or above (required for agent features)
- Git (to clone and keep the repository up to date)

---

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/ricardomcruz/surf-coach.git
cd surf-coach
```

### 2. Open in Claude Code

```bash
claude
```

### 3. Start coaching

```
/coach
```

The coach detects where you are. On first run, it explains the system and guides you through setup step by step. You don't need to know anything else to begin.

---

## Recommended first-use flow

`/coach` automatically detects missing data and guides you — but if you prefer to set up in the optimal order:

```
/setup-profile     → who you are as a surfer
/setup-goals       → 1 to 3 concrete goals
/setup-metrics     → health and performance baselines
/setup-activities  → what you train out of water and when
/plan-gym          → structured gym program (A/B/C session types)
/setup-nutrition   → nutritional profile and preferences
/plan-week         → plan your first week
```

Then: go surf → `/log-session` → return to `/coach`. Repeat.

---

## Available commands

| Command | What it does |
|---|---|
| `/coach` | **Start here.** Reads everything and coaches you based on your actual data |
| `/log-session` | Log a surf session — right after surfing |
| `/plan-week` | Plan the full week: forecast, surf sessions, gym, meals, shopping list |
| `/consult [topic]` | In-depth multidisciplinary consultation on a specific topic (recovery, technique, mental health, habits, periodization) — 3 to 4 specialists in sequence, each reading what the previous one wrote |
| `/spiritual` | Direct conversation with the spiritual guide — presence, your relationship with the ocean, what surfing means |
| `/setup-profile` | Configure or update your surfer profile |
| `/setup-goals` | Set or update goals |
| `/setup-metrics` | Log health and performance metrics |
| `/setup-activities` | Log available training activities and time slots |
| `/plan-gym` | Create structured gym program (strength, functional, active recovery) |
| `/setup-nutrition` | Configure nutritional profile and food preferences |
| `/evolve` | Audit and improve the coaching system itself — run every 4–8 weeks |
| `/reset` | Clear all athlete data (to restart or switch to a new user) |

---

## The specialists

`/coach` orchestrates a team of 14 background specialists:

| Specialist | Domain |
|---|---|
| Psychologist | Mental performance, stress, motivation, life-surf balance |
| Mobility Coach | Posture, movement quality, yoga, technique blockers |
| Nutritionist | Sports nutrition, body composition, recovery nutrition |
| Gym Coach | Strength & conditioning, training load, periodization |
| Surf Technique Coach | Technical analysis, maneuver biomechanics, progression |
| Breathing Coach | Functional breathing, CO2 tolerance, hold-down prep |
| Sleep Specialist | Sleep science, chronobiology, sleep architecture |
| Physiotherapist | Injury prevention, prehab, musculoskeletal loading |
| Periodization Coach | Long-term training arc, mesocycles, swell windows |
| Life Coach | Habit formation, daily routines, behavioral change |
| Health Coach | Biohacking, supplementation, longevity, HRV, systemic inflammation |
| Chinese Medicine Doctor | TCM patterns, energetic balance, seasonal rhythms |
| Psychosomatic Doctor | Mind-body patterns, somatic stress expression |
| Spiritual Guide | Presence, contemplative practice, ocean relationship |

Specialists read each other's reports before writing their own — the physiotherapist knows what the gym coach prescribed, the health coach knows what the sleep specialist identified. The surf coach synthesizes it all.

---

## Weekly plan in HTML

`/plan-week` automatically generates an HTML page of your weekly plan in `public/plans/`. It includes forecast, surf sessions, workouts, meals, and shopping list — optimized for your phone before a session, at the gym, or at the supermarket.

The system improves itself every week: after generating the plan, a review agent reads the page, identifies usability issues, and updates the design spec for next week.

---

## Your data

Everything that's yours lives in the `private/` folder on your computer. It's not sent anywhere, not shared, not in git. The coaching system (skills, agents, config) is shareable — your data is not.

```
private/
  data/
    sessions/          → one file per surf session
    goals/             → active goals
    profile/           → surfer profile
    metrics/           → health and performance snapshots
    plans/             → weekly plans in markdown and HTML
    specialist-reports/→ specialist assessments per session
    activities.md      → available training and time slots
    gym-programme.md   → gym program
    nutrition-profile.md → nutritional profile
```

---

## Getting the most out of it

1. **Log sessions right after surfing.** While it's fresh. With honesty — what didn't go well matters as much as what did.
2. **Set up carefully.** The first steps can feel slow. They're not. Every field you fill makes every future session more precise.
3. **Come back regularly.** Value accumulates over time. Three months of data is qualitatively different from three weeks.
4. **Bring real questions.** Physical, mental, technical, life — the system is built for complexity.
5. **Use `/consult` when something persists.** If there's a pattern that won't resolve, a recurring injury, or a mental block — the consultation mode goes deeper than `/coach` generalizes.

---

## The philosophy

The best coaching isn't the most enthusiastic. It's the most precise. A coach that knows you — your patterns, your avoidances, your real capacity versus what you claim — can say less and mean more.

That's what this system is designed to be.
