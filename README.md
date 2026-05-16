# Lift
Weightlifting PWA

A minimalist weightlifting tracker built as a single-file progressive web app. Designed for hip hinge, glute, and posterior chain training with a barbell, dumbbells, a squat rack, and resistance bands. Pin it to your iPhone home screen and it works like a native app — no App Store, no account, no internet required.

---

## Features

### Workout Logging
Log sets by weight and reps (or seconds for timed holds). Supports multiple exercises per session. A 3-minute rest timer starts automatically after each set, with haptic vibration and an audio beep when time is up.

### Progressive Overload Engine
Every exercise remembers your last session. When you open an exercise, the app pre-fills the suggested weight and reps based on your history: if you hit your target reps last time, it bumps the weight by 5 lbs. If you fell short, it holds you at the same weight. Banded and bodyweight exercises progress by reps instead of load. Timed exercises (Dead Hang) progress by 5 seconds.

### Weekly Plan
A structured A/B weekly program that alternates automatically by calendar week. Each day shows the prescribed exercises, sets, reps, a form cue, and your suggested weight pulled live from your history. One tap loads the day's workout into the logger. Write a weekly intention at the top of the plan — it saves per week and resets automatically.

### Workout Calendar
A monthly calendar that circles every day you logged a workout in green. Navigate forward and backward through months. A count of workouts for the displayed month is shown below the grid.

### History
A reverse-chronological log of every finished workout. Each entry shows the date, total sets, and total volume (weight × reps). Tap to expand and see the full set-by-set breakdown. History accumulates indefinitely and is never auto-cleared.

---

## Exercise Library

All exercises are scoped to this equipment: 25 lb barbell, bumper plates (5/10/15/25 lb), squat rack, adjustable dumbbells up to 50 lb, pull-up resistance bands, knee bands.

| Category | Exercises |
|---|---|
| Hip Hinge / Glute — Barbell | Romanian Deadlift, Good Morning, Rack Pull, Hip Thrust |
| Hip Hinge / Glute — Dumbbell | Romanian Deadlift, Single-Leg RDL, Hip Thrust, Sumo Squat (goblet) |
| Hip Hinge / Glute — Banded | Hip Thrust, Clamshell, Glute Kickback, Lateral Walk |
| Posterior Chain — Pull-Up Bar | Pull-Up, Band-Assisted Pull-Up, Band-Assisted Chin-Up, Dead Hang |
| Posterior Chain — Barbell | Row (overhand), Row (underhand), Shrug |
| Posterior Chain — Dumbbell | Single-Arm Row, Shrug, Rear Delt Fly, Face Pull |

---

## Installation

### Pin to iPhone (Recommended)

1. Open `index.html` from any static host in **Safari**
2. Tap the Share button → **Add to Home Screen**
3. Tap **Add**

The app runs fully offline from that point. No internet connection needed after the first load.

### Run Locally

```bash
# Any static file server works. Examples:

npx serve .
# or
python3 -m http.server 8080
```

Then open `http://localhost:8080` in Safari and add to home screen.

### Deploy (One-Command Options)

```bash
# Netlify Drop — drag the folder to netlify.com/drop

# Vercel
npx vercel .

# GitHub Pages — push to a repo, enable Pages in Settings → Pages → Deploy from branch
```

---

## Technical Notes

**Single file.** The entire app — HTML, CSS, JavaScript — lives in `index.html`. No build step, no dependencies, no CDN calls.

**Storage.** All data is saved to `localStorage` under the key `lift_v1`. Weekly intentions are saved separately as `lift_intention_{year}_w{weekNumber}`. Nothing leaves the device.

**Data shape.**
```json
{
  "unit": "lbs",
  "workouts": [
    {
      "date": "2026-05-16",
      "exercises": [
        {
          "name": "Romanian Deadlift (barbell)",
          "sets": [
            { "weight": 95, "reps": 8, "seconds": null }
          ]
        }
      ]
    }
  ]
}
```

**PWA manifest.** Injected at runtime as a blob URL so the app stays truly single-file and works when opened directly from the filesystem.

**Audio.** Rest timer beep is generated via the Web Audio API — no audio files required.

**Vibration.** Uses `navigator.vibrate()`. Supported on Android and some iOS versions (iOS 17+). Fails silently if unsupported.

---

## Weekly Program Structure

The app rotates between two programs by calendar week number.

**Week A — Hip Hinge Heavy + Pull Strength**
- Monday: Barbell RDL, Dumbbell Hip Thrust, Banded Glute Kickback, Banded Clamshell
- Wednesday: Pull-Up, Barbell Row (overhand), Single-Arm DB Row, Rear Delt Fly
- Friday: Good Morning, Single-Leg RDL, Band-Assisted Pull-Up, Banded Hip Thrust

**Week B — Volume + Unilateral Emphasis**
- Monday: Banded Hip Thrust, Dumbbell RDL, Sumo Squat, Banded Lateral Walk
- Wednesday: Band-Assisted Chin-Up, Barbell Row (underhand), Dumbbell Face Pull, Dumbbell Shrug
- Friday: Rack Pull, Single-Leg RDL, Pull-Up, Banded Clamshell

---

## Browser Support

| Browser | Support |
|---|---|
| Safari on iOS | ✅ Full — recommended |
| Safari on macOS | ✅ Full |
| Chrome on Android | ✅ Full |
| Chrome on desktop | ✅ Full (no vibration) |
| Firefox | ✅ Full (no vibration on iOS) |

---

## License

MIT
