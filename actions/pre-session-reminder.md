# Action: Pre-session reminder

Use this action when sending the evening-before reminder for a training session — typically triggered by the daily 18:00 scheduled task, or when the athlete asks "what's the session tomorrow / what should I be thinking about."

## Steps

1. **Read tomorrow's calendar event** for the training session. The event description is the source of truth for what's prescribed.

2. **Pull cycle context** for tomorrow's date (`mcp__garmin__get_menstrual_data_for_date` or `mcp__garmin__get_menstrual_calendar_data`). Name the phase if it's meaningfully relevant to tomorrow's session — particularly for race-effort or high-intensity sessions.

3. **Compose the reminder** per the format below. If cycle phase warrants an adjustment (race day in late luteal phase = adjust expectations and pacing strategy), surface that.

4. **If a material adjustment is needed**: propose the adjustment, ask the athlete to confirm before changing the calendar event.

**Note on weather:** the Cowork environment can't reach external forecast APIs (no general weather MCP, WebFetch URL provenance blocks Open-Meteo). Weather context lives in *post-session* reviews, where Garmin's `get_activity_weather` provides reliable historical data. Skip it in the reminder. If conditions look extreme on the day, the athlete can flag in chat and you can adjust.

## Reminder structure

```
**Tomorrow [day] [HH:MM] — [Session type, distance, key target]**

[1-line headline: what this session is for]

**Targets:** [paces, loads, effort caps — pulled from the calendar event]

**Cycle context:** [phase + practical implication — only if relevant to the session type]

**Form / safety note:** [one specific thing — HR cap, breath-holding on lifts, eyes forward, calf check, etc.]

**Track:** [one thing to pay attention to — avg HR for easy runs, splits for parkrun, RPE for tempo, loads for gym]
```

Length scales with session complexity:
- Easy run: 3–5 lines total
- Tempo / quality run: 6–10 lines
- Race-effort parkrun: 6–10 lines with explicit pacing strategy
- Long run: 6–10 lines including fuelling note
- Gym session: list of exercises with this week's loads pulled from the calendar event

## How cycle phase should shape the reminder

- **Menses (days 1–~5):** if she finds it tough, expect higher RPE; otherwise normal. Many athletes train well in this phase.
- **Mid-follicular (days ~7–13):** highest energy / output phase. Best window for race efforts, PBs, hard intervals. If race effort lands here, say so positively.
- **Ovulation (~14):** can be a temporary HR spike — note if it's a hard day.
- **Luteal (days ~15–28):** mid-luteal often fine; **late luteal (~days 26–30)** is the lowest-output phase. Race efforts here should expect slower times, HR climbing faster. Calibrate expectations explicitly.

Use cycle context to set realistic expectations and adjust pacing strategy. Don't use it as an excuse — name what to do about it.

## What to skip

- Don't restate the entire event description back to her.
- Don't add weather/cycle context if neither is material.
- Don't include all four optional sections every time — they're conditional.
- Don't add cheerleading.

## Example — Friday tempo, mid-follicular phase

> **Tomorrow 07:00 — 12km with 5km tempo block @ 4:40–4:45/km**
>
> First proper quality session of the block. The middle 5km should feel comfortably hard, not redlining.
>
> Targets: 3km easy warm-up at 6:10/km → 5km @ 4:40–4:45 → 4km easy cool-down at 6:10. If the middle 5km lactic-burns, dial to 4:50/km and note it.
>
> Form note: settle pace by 1km mark of the tempo block — don't go out at 4:30/km.
>
> Track: can you hold target pace evenly across all 5 reps, or did pace fade?

## Example — Saturday parkrun race effort, late luteal phase

> **Tomorrow 09:00 — Parkrun RACE EFFORT (target sub-22:00)**
>
> Fitness checkpoint for the block.
>
> Targets: km 1 at 4:22–4:24 (hard ceiling 4:20), settle 4:18–4:22 km 2–4, empty the tank km 5.
>
> Cycle context: late luteal phase (day 28). Expect HR to climb 5–10 bpm faster than normal; perceived effort will be higher at any given pace. Plan for this — start conservatively, and a target of 22:10–22:20 is more realistic than 21:50.
>
> Form note: hydrate well tonight, breakfast 2.5h before start as usual.
>
> Track: split shape (positive split = went out too hot, negative = paced well), and how the last km felt.
