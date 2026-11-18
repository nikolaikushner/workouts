# Workouts

A personal gym tracker for a 4-day split. One HTML file, no backend, no build step. Hosted on GitHub Pages.

**Live:** https://nikolaikushner.github.io/workouts/

## Features

- **4-day split** — upper push, lower body, upper pull, legs + conditioning. Each exercise shows the working weight and the sets × reps scheme.
- **Warm-up run** — every day starts with a 1 km run on the treadmill. It has its own check box above the exercise list.
- **Set checklist** — tap a set number to mark it done. An exercise turns green when all its sets are done.
- **Progress calendar** — the Stats tab shows a month calendar. A day turns green when at least one set is checked, with a D1–D4 label for the workout. Also shows workouts this week, this month and all time, plus a list of recent sessions.
- **English and Russian** — EN/RU switch in the header. English is the default.
- **Light and dark theme** — follows the system setting.
- **Mobile first** — built for a phone in the gym. Add it to the home screen to open it like an app.

## How data is stored

Everything lives in the browser's `localStorage`. Nothing is sent anywhere.

| Key | Content |
| --- | --- |
| `lang` | `"en"` or `"ru"` |
| `day` | Last opened tab |
| `checks-day1` … `checks-day4` | Set checks for the current date: `{ date, sets }` |
| `log` | Workout log: `{ "2026-10-21": { "day1": 5 } }` — sets checked per workout per date |

Set checks reset on a new date. The log keeps the history for the calendar.

Clearing site data or opening the page on another device starts with an empty calendar.

## Editing the plan

All workouts are in the `DAYS` array in `index.html`. Each exercise is:

```js
[["English name", "Русское название"], weight_kg, ["scheme EN", "scheme RU"], set_count, ["note EN", "note RU"]]
```

Use `null` for the weight when an exercise has no load (plank, cardio). The note is optional. When a scheme is the same in both languages, one value is enough: `["4×10"]`.

UI text is in the `T` object, one block per language.

## Body weight

The Stats tab also shows body weight: start, current, change, BMI and progress to the 72 kg goal. The weigh-ins are in the `BODY` object in `index.html`:

```js
const BODY={height:166,goal:[68,72],log:[
 ["2026-05-11",81.1],
 ["2026-11-09",74.2]
]};
```

Add a new row at the end of `log` for each new weigh-in.

## Progression rules

- Each week add 1–2 reps or 2.5 kg.
- When you reach the top of the range in all sets, add weight and start again from the bottom of the range.
- 45–60 minutes per session.
- Cardio separately: walking 40–60 minutes on rest days.

## Tech

Plain HTML, CSS and JavaScript in one file. Fonts from Google Fonts (Barlow Condensed, IBM Plex Sans).
