# Running Coach Skill

A Claude Code skill that acts as a personal running coach. It reviews Garmin sessions, builds weekly previews, plans training blocks, prepares you for race day, and answers ad-hoc training questions — all grounded in your specific athlete profile, training philosophy, and live calendar data.

## What it does

The coach triggers automatically when you ask anything training-related: reviewing a run, discussing pacing, asking about a niggle, planning next week, or preparing for a race. It reads your Garmin data, Google Calendar events, and a persistent training journal to give specific, data-grounded advice rather than generic guidance.

Five structured actions cover the main use cases:

| Trigger | Action |
|---|---|
| "Review my run" / new Garmin activity | Session review with splits, HR zones, conditions, cycle context |
| "What's the plan tomorrow" | Evening pre-session reminder |
| "What's the plan this week" / Sunday recap | Weekly preview |
| End of training block / "plan next block" | New block planning |
| <3 weeks to race / "race day strategy" | Race prep and taper guidance |

## Directory structure

```
running-coach/
├── SKILL.md                  # Main skill definition — triggers, routing, style rules
├── athlete-profile.md        # Athlete-specific data (gitignored — see setup)
├── training-philosophy.md    # Coaching principles (athlete-agnostic)
├── actions/
│   ├── review-session.md     # How to review a logged Garmin session
│   ├── pre-session-reminder.md
│   ├── weekly-preview.md
│   ├── plan-next-block.md
│   └── prep-race.md
└── evals/
    └── evals.json
```

Two additional files live **outside** this folder and are referenced by the skill:

- **Active training plan** — a markdown file per training block (e.g. `oxford-half-training-block-1.md`), kept alongside your other running documents
- **Training journal** — an append-only log (`training-journal.md`), where every session review is stored; the coach reads the last 10–20 entries before any review

## Required integrations

The skill depends on two MCP servers being available in your Claude Code environment:

- **Garmin MCP** — for activity data, splits, HR zones, weather, and menstrual/cycle data. Recommended: [taxuspt/garmin_mcp](https://github.com/taxuspt/garmin_mcp)
- **Google Calendar MCP** — for reading and (with your confirmation) updating scheduled training sessions

Without these, the coach can still answer ad-hoc questions and read your training files, but session reviews and calendar-aware features won't work.

## Setup

### 1. Copy the skill folder

Place this folder wherever you keep your Claude Code skills. The exact location doesn't matter, but you'll reference it in the next step.

### 2. Update the hardcoded paths in `SKILL.md`

Two absolute paths in `SKILL.md` need to match your own machine. Search for the `## Persistent context` section and update:

**Active training plan** — replace the example path with wherever you want your training block files to live (e.g. `~/Documents/running/oxford-half-block-1.md`). The coach will create this file when you ask it to plan your first block, and you update the path each time a new block starts.

**Training journal** — replace the example path with wherever you want the append-only session log to live (e.g. `~/Documents/running/training-journal.md`). The coach creates and maintains this file automatically.

### 3. Install the required MCPs

Make sure both MCP servers are configured in your Claude Code environment before your first session.

### 4. Start a conversation — the coach handles the rest

On first run, the coach will detect that `athlete-profile.md` is missing and interview you to build it. It asks one topic at a time: goals, medical history, weekly schedule, known tendencies, equipment. Once confirmed, it saves the file.

After that, ask the coach to plan your first training block. It will:
- Draft a 4-week block based on your goal race and current fitness
- Create Google Calendar events for each session (with your confirmation before anything is created)
- Set up the training journal

From that point, the coach is self-maintaining: it appends journal entries after every session review, updates the training plan file as blocks change, and proposes calendar updates when the data warrants it.

## How confirmation works

The coach distinguishes between things it can do freely and things it must ask you about first.

**No confirmation needed:**
- Reading Garmin data, calendar events, journal entries, plan documents
- Sending reviews, reminders, previews, and advice
- Appending to the training journal

**Always asks first:**
- Any change to a calendar event
- Any change to weekly volume targets
- Adding, removing, or moving sessions
- Recommending a rest day that's not in the original plan

When proposing a change, the coach states what and why in 1–2 sentences, then waits for a yes or no before acting.

## Adapting the coaching philosophy

`training-philosophy.md` is intentionally athlete-agnostic. The principles in it (80/20 polarisation, injury prevention as the meta-goal, cutback weeks, HR vs pace by session type) apply broadly. You can edit it if your approach differs — for example if you follow a different intensity distribution model or have different views on strength training frequency.

Changes to philosophy take effect immediately on the next coaching interaction; nothing needs to be reset or reloaded.

## Coaching for a different athlete

The only file you need to swap is `athlete-profile.md`. Everything else (the skill logic, philosophy, action files) is athlete-agnostic. You'd also update the two paths in `SKILL.md` to point to the new athlete's plan and journal files.
