# Surf Coach

A personalized AI-powered surf coach that helps you plan, track, and improve your surfing through a set of intelligent agents and skills.

## What it does

Surf Coach acts as your personal surf coach — it helps you:

- Define and track your surf goals
- Log and review surf sessions
- Analyse your progression over time
- Plan training based on conditions, location, and your current level
- Get personalised advice to reach your objectives faster

## Structure

```
surf-coach/
├── agents/         # Autonomous agents (e.g. session analyser, goal tracker)
├── skills/         # Claude Code skills for specific coaching tasks
├── data/
│   ├── sessions/   # Surf session logs
│   ├── goals/      # Your surf goals and milestones
│   └── profile/    # Your surfer profile (level, boards, home break, etc.)
├── config/         # Configuration and settings
└── docs/           # Documentation and guides
```

## Getting started

1. Fill in your surfer profile in `data/profile/`
2. Set your goals in `data/goals/`
3. Start logging sessions in `data/sessions/`
4. Run skills and agents via Claude Code to get coaching insights

## Philosophy

Every surfer is different. This coach adapts to your level, your home break, your board quiver, and your goals — whether you're learning to pop up or chasing barrels.
