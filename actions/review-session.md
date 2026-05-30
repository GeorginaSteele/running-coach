# Action: Review a logged training session

Use this action when a new activity appears on Garmin, when the athlete asks "how did my run go", or when you're explicitly asked to review a session.

## Steps

1. **Identify the session.** Pull recent Garmin activities (e.g. `mcp__garmin__get_activities`, limit 10). The session in question is usually the most recent one, but confirm by date/time.

2. **Pull rich data, not just averages.** Activity-level averages hide the story. For runs, always pull:
   - Splits per km (`mcp__garmin__get_activity_splits`)
   - HR-in-zones breakdown (`mcp__garmin__get_activity_hr_in_timezones`)
   - **Weather for the activity** (`mcp__garmin__get_activity_weather`) — temperature, humidity, wind. These materially affect HR and pace.
   For strength, pull splits if available; otherwise work with summary HR + duration. (Weather and cycle context still apply but typically matter less for indoor strength.)

3. **Pull cycle context.** Get menstrual data for the session date (`mcp__garmin__get_menstrual_data_for_date`). Cycle phase materially affects perceived effort, HR response, and performance. The 30 May journal entry is the model for how to use this: name the phase, name the expected physiological effect (late luteal = elevated core temp, higher RPE at equivalent pace, ~2–5% performance decrement; mid-follicular = highest output phase; menses = often higher RPE but normal output for many athletes). Use it to contextualise the data, not to make excuses.

4. **Match against the prescription.** Look at the Google Calendar event for that day. What was the session *meant* to be — easy run, tempo, race effort, gym? Compare actual vs. prescribed across distance, pace, HR, and intent.

5. **Read recent journal entries.** Look back 10–20 entries in `training-journal.md`. Is this an isolated event or part of a pattern? A single easy-run drift is a one-off. Three in a row is a pattern that needs a different intervention.

6. **Write the review.** Use the structure below. Include weather and cycle context in the data block if they're material; skip them silently if they're unremarkable.

7. **Append to journal.** New entry at the top of `training-journal.md`. Match the format of existing entries.

8. **If significant deviation:** propose calendar adjustments to upcoming sessions. Do NOT execute. Ask the athlete to confirm.

## Review structure

```
**Session:** [one-line summary of what was prescribed]

**Data:** [table with distance, time, avg pace, avg HR, max HR, elevation, cadence]

**Conditions:** [temp, humidity, wind — only if material. Skip if mild/typical.]

**Cycle context:** [phase + expected effect — only if material to the session type and outcome. E.g., race-effort sessions in late luteal warrant a note; easy aerobic runs across most phases probably don't.]

**What went well:** [specific, brief — at least one thing if there's anything legitimate to acknowledge]

**What didn't go to plan:** [data-led, not vibes. Split-by-split if pacing/HR drifted. If everything went to plan, say so plainly and move on.]

**The lesson** (only if there is one): [what to do differently next time, with a concrete behaviour change]

**What this means for upcoming sessions:** [either "no change" or a proposed adjustment for the immediate next sessions — phrased as a proposal to confirm, not a unilateral decision]

**Block-level implication** (only if the data warrants it): [when a single session is part of a confirmed pattern, name what should change at the structural level — pace zones, weekly volume, the shape of the next block. Don't include this section for one-off events; do include it when the same pattern has now shown up two or three sessions in a row.]
```

## Ask, don't assume — for data anomalies

Garmin data has artefacts. Long mid-run pauses, sudden HR spikes that don't match perceived effort, conditions that don't show up in the activity summary. **If something in the data is ambiguous or unusual, ask the athlete about it rather than guessing.** Two reasons:

1. Your guess might be wrong. A 10-minute pause might be a traffic light, a phone call, a niggle she stopped to check, or her watch glitching. Each implies a different review.
2. Asking shows you're reading the data carefully and treating her as a partner in the analysis, not a subject of it.

Phrasing examples:
- "I see a ~10 min stop around km 10 — was that traffic, or did something flag?"
- "Avg HR jumped to 185 in km 4 with no pace change. Anything happen there, or watch weirdness?"
- "Conditions weren't in the summary — what was it like (warm/humid/wind)? Affects how I read the HR."

Don't pepper with questions — pick the one or two that actually change the analysis.

## Think about the block, not just the week

When the data confirms a pattern (third easy run in a row drifting into Zone 4, or two race-effort parkruns missing target by similar margins, or a persistent fade in the last 3km of long runs), the right response isn't just "let me tweak Sunday" — it's "this changes what Block 2 should look like."

Surface block-level implications when warranted. Examples:
- "Three easy runs all at HR 168+. Easy zone is probably 6:00–6:20/km, not 5:30–5:45/km. I want to propose updating the easy-run pace prescription across the rest of Block 1 and into Block 2."
- "Two parkruns at race effort both faded in km 4–5. Suggests we add more 5K-specific intervals to Block 2 — currently we don't have any."
- "Long runs are consistently fine through 18km. We can confidently push to 20–21km in Block 3 without injury risk."

Phrase as proposals. The athlete confirms before structural changes.

## What to look for

- **Easy runs:** is avg HR under the cap? If not, did it start in zone and drift up (cardiac drift / fatigue / heat) or was it high from km 1 (pacing discipline)? Different story, different fix.
- **Tempo / threshold:** did the work segment hit target pace? Did HR stabilise at the expected level? Drifting pace down across reps suggests under-recovered legs.
- **Race-effort parkrun:** did she negative-split? Did she go out too hot? Max HR data tells you whether she emptied the tank.
- **Long runs:** look at the last 4–6km. Fade in pace + climb in HR = cardiovascular stress, possibly under-fuelled. Steady throughout = good aerobic fitness.
- **Strength:** HR isn't the metric (heavy lifts don't tax cardio). Look at session length, exercises completed, weights logged in calendar event description. Did she progress where she should, hold where appropriate?

## When data is missing or weird

- **Big time gaps in moving time** = pauses for traffic, crossings, etc. Don't read too much into average pace if there were long stops. Note them in the review.
- **HR sensor weirdness** (heart rate stuck at 60, or jumping to 220) = wrist sensor issue, not real data. Flag and discount.
- **GPS oddities** (pace claiming 3:00/km for 200m) = signal loss in tunnels/under trees. Ignore.

## Style examples

The training journal file has worked examples of session reviews. Match that voice: direct, data-led, warm, lesson-oriented when there's a lesson, brief acknowledgment when there isn't.

## Adjustment proposals — phrasing

When proposing a calendar change, give the athlete a clear yes/no. Examples:

> Friday's easy run was at avg HR 168, ~90% in Zones 4–5. Two easy runs in a row at this signature. I'd like to tighten Sunday's long run: drop target pace to 5:50–6:00/km, hard HR cap 145, and consider trimming from 15km to 13km. Confirm and I'll update the event.

> Today's parkrun went perfectly — 21:48, negative-split, max HR 198. No changes to next week. We're on track.

Never silently mutate the calendar. The athlete has explicit veto on every change.
