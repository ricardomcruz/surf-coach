---
name: consult
description: Multidisciplinary consultation. Invokes 3-4 specialists sequentially on a specific topic — each specialist reads what the previous ones wrote in this session before contributing. Produces richer, non-contradictory reasoning than parallel invocation. Use when a problem has clear roots in multiple domains simultaneously.
---

You are coordinating a multidisciplinary consultation. This is different from a normal coaching session — specialists run **sequentially**, not in parallel. Each one reads what the previous specialists produced in this session before writing their own contribution. The result is layered reasoning, not isolated reports.

---

## Step 1 — Read context

Before selecting specialists, read:
1. `private/data/profile/profile.md`
2. `private/data/goals/goals.md`
3. `private/data/sessions/summary.md` if it exists, or the most recent 3 session logs
4. List `private/data/specialist-reports/` — read the most recent `latest.md` from each specialist that has one. These give you background context.
5. The topic passed as argument (e.g., `/consult recovery`, `/consult technique`, `/consult mental health`)

---

## Step 2 — Select specialists for this topic

Based on the topic, select 3–4 specialists in the order they should contribute. The sequence matters: more foundational specialists go first, so downstream specialists can build on their output.

Use these groupings as a guide — adapt based on what the athlete's data actually suggests:

**Recovery / Recuperação**
Sequence: `sleep-specialist` → `health-coach` → `gym-coach` → `psychologist`
When: persistent fatigue, poor HRV trend, non-restorative sleep, overtraining signals

**Technique / Técnica**
Sequence: `mobility-coach` → `physiotherapist` → `surf-technique-coach` → `breathing-coach`
When: technique plateau with possible physical roots, recurring mechanical breakdown, take-off or manoeuvre stuck for multiple sessions

**Mental performance / Saúde mental**
Sequence: `psychologist` → `psychosomatic-doctor` → `life-coach` → `spiritual-guide`
When: motivation patterns, stress-body dynamics, habit consistency, meaning and presence

**Physical health / Saúde física**
Sequence: `physiotherapist` → `health-coach` → `nutritionist` → `gym-coach`
When: injury risk, systemic inflammation, supplementation questions, load management

**Habits / Hábitos**
Sequence: `life-coach` → `psychologist` → `sleep-specialist` → `health-coach`
When: consistency gaps between intention and behaviour, routine breakdown, lifestyle change

**Periodisation / Periodização**
Sequence: `periodisation-coach` → `gym-coach` → `physiotherapist` → `psychologist`
When: phase transitions, seasonal planning, goal deadlines approaching, training arc questions

**Custom:** If the topic doesn't match a grouping, select 3–4 specialists based on domain relevance and sequence them from most foundational (structural, physical) to most integrative (psychological, systemic).

---

## Step 3 — Run the consultation sequentially

Invoke the first specialist using the Agent tool. Pass them:
- The topic of the consultation
- All relevant athlete data files to read
- An explicit instruction: "This is a multidisciplinary consultation. Read the athlete's data files AND the consultation thread below (if it exists). Add your specialist perspective, building on what previous specialists wrote rather than repeating it. Be concise — under 200 words. Flag agreements, contradictions, and anything the previous specialists missed from your domain."
- The consultation thread so far (initially empty, grows with each specialist's output)

Wait for the first specialist's output. Then invoke the second specialist, passing the growing consultation thread. Continue until all selected specialists have contributed.

**Consultation thread format:**
```
## [Specialist Name] — [date]
[Their contribution — max 200 words]
```

---

## Step 4 — Synthesise

After all specialists have contributed, write a synthesis:

**Consultation: [Topic] — [Date]**

**What converges:** [Points all or most specialists agreed on — these are high-confidence findings]

**What diverges:** [Points where specialists had different reads — name the tension explicitly and give your coaching judgment on how to resolve it]

**The single most important thing to address:** [One clear priority that emerges from the full consultation]

**Recommended actions:**
- [Action 1 — specific, attributed to the specialist who identified it]
- [Action 2]
- [Action 3 if warranted]

---

## Step 5 — Save the record

Write the full consultation to:
`private/data/consult/YYYY-MM-DD-[topic].md`

Include: topic, specialists consulted, full consultation thread, and your synthesis.

Create the `private/data/consult/` directory if it doesn't exist.

---

## When to use /consult vs /coach

`/coach` — regular coaching session. Specialists run in parallel from cached reports. Fast, broad, appropriate for most sessions.

`/consult [topic]` — focused deep-dive. Specialists run sequentially, each reading the others in real time. Slower, deeper, for problems with clear multi-domain roots.

The coach should suggest `/consult` when:
- A problem has been present across 3+ sessions without resolution
- Multiple specialists have flagged the same domain from different angles
- The athlete raises a topic that is clearly multi-domain (e.g., "my recovery is not improving despite sleeping more")
- A significant life or training transition is happening
