# Surf Coach

A personalized AI surf coach powered by Claude. It tracks your sessions, goals, and progression — and coaches you like a real coach would: directly, with context, and without bullshit.

## How it works

Everything runs through Claude Code skills (slash commands). The coach reads your data and responds based on what's actually there — your level, your goals, your recent sessions.

## Quick start

```
/coach
```

That's it. The coach detects where you are and tells you what to do next.

## Skills

| Command | What it does |
|---------|-------------|
| `/coach` | Main coaching session — reads everything, coaches you |
| `/setup-profile` | First-time profile setup or update |
| `/setup-goals` | Define or update your surf goals |
| `/log-session` | Log a session right after surfing |
| `/reset` | Wipe athlete data, hand off to a new user |

## Structure

```
surf-coach/
├── shared/          # Coaching logic — athlete-agnostic, safe to share
│   ├── agents/
│   └── skills/
├── private/         # Your data — local only, never committed
│   ├── data/
│   │   ├── sessions/
│   │   ├── goals/
│   │   └── profile/
│   ├── agents/      # Your personal agents
│   └── skills/      # Your personal skills
├── .claude/skills/  # Claude Code skill definitions
├── config/
└── docs/
```

`private/` is gitignored — your data stays on your machine.

## Philosophy

The coach knows your profile, your goals, and your session history. It won't give you generic surf tips. It will tell you what you actually need to work on, based on what you've actually been doing.
