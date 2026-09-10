# Product Requirements Document

## Side Quests  — *See Through My Eyes*

| Field | Value |
| --- | --- |
| Version | 2.0 |
| Status | Implemented |
| Platform | Progressive Web App (mobile-first) |
| Cycle length | 11 days (Thu 10/09 - Sun 20/09) |

---

## 1. Overview

**Side Quests Vol. III** is an eleven-day, two-person creative experience delivered as a single-page PWA. Each day unlocks one photo/thought prompt at a synchronized, pseudo-random time. Participants capture a response, compose a branded share card locally on their phone, and send it to each other outside the app.

**Tagline:** *One prompt a day, at an hour neither of you picks.*

The product is intentionally lightweight: no accounts, no backend, no uploads. Everything runs in the browser and stays on the device.

---

## 2. Problem & Goals

### Problem

- Daily communication between two people can become repetitive and lack intentional moments of sharing.
- Messaging apps provide no structure and no sense of shared anticipation.

### Goals

| Goal | Description |
| --- | --- |
| Intentional connection | One prompt per day, no streak pressure |
| Synchronized experience | Both people unlock at the same minute |
| Privacy by design | Photos are composed and stored only on-device |
| Cinematic UX | Theater-inspired visuals, Hero Calendar Grid, interactive entrance rituals |

---

## 3. Target Users

- **Primary:** Couples or close friends who want a daily creative ritual together.
- **Secondary:** People who enjoy photo-based journaling with a structured prompt.
- **Device:** Mobile-first (iOS/Android), installed via Add to Home Screen.

---

## 4. User Flow

```
Hero (Day X + 11-Day Calendar Grid)
    ↓
Before unlock time → Countdown ("Doors Closed")
    ↓
At unlock time → Complete day-specific Entrance Ritual → Prompt opens
    ↓
Scroll → Day-specific reveal animation
    ↓
Read mission → Take or choose a photo / write thought
    ↓
Compose branded card → Share or Save
    ↓
Mark day as answered (localStorage) + View post-posting reflection quote
    ↓
"Tomorrow" — wait for the next day
```

---

## 5. Core Features

### 5.1 Hero Calendar Grid
- Placed prominently in the Hero section.
- Displays the 11-day date range: **Thursday 10/09 to Sunday 20/09**.
- Automatically highlights the current active day with a glowing crimson state, while tracking answered/completed days.

### 5.2 Time-Based Unlock
- The daily window runs from **7:00 to 22:00** local time.
- Unlock time is computed with a **seeded algorithm** (Fisher–Yates band shuffle) across the 11 days so both devices show the exact same minute for the same calendar day.
- Before unlock: full-screen countdown with `hh:mm:ss` clock.

### 5.3 Entrance Rituals (All 11 days)

Each day has an interactive ritual mini-game to unlock the prompt:

| Day | Date | Ritual Name | Interaction |
| --- | --- | --- | --- |
| 1 | Thu 10/09 | The Charge | Press and hold battery for 5 seconds to charge |
| 2 | Fri 11/09 | The Everyday Machine | Wipe/swipe away static noise on an ordinary object |
| 3 | Sat 12/09 | The Listening Room | Listen to a faint sound cue, then tap "I HEARD IT" |
| 4 | Sun 13/09 | The Three Doors | Pick one of 3 doors (THEN, THERE, SOMEWHERE) to peek and unlock |
| 5 | Mon 14/09 | Kindness Radar | Tap moving dot when it enters radar center (3 times) |
| 6 | Tue 15/09 | Zoom Out | Press & hold for 5 seconds to zoom out from person to world |
| 7 | Wed 16/09 | The Ladder | Drag progress marker to exactly 1% |
| 8 | Thu 17/09 | The Three Paths | Choose a path outside your normal routine (MAYBE or WHY NOT?) |
| 9 | Fri 18/09 | The Locked Letter | Rotate 3 lock rings to unlock envelope (SAY / SHOW / KEEP) |
| 10 | Sat 19/09 | Save This | Drag bookmark/star into camera frame |
| 11 | Sun 20/09 | Time Capsule | Drag glowing dot into box to seal for 1 year |

### 5.4 Daily Prompts & Reflections

Each day contains mission text, word requirements, reveal animation, and a post-posting reflection:

| Day | Codename | Subtitle | Words | Theme |
| --- | --- | --- | --- | --- |
| 1 | Energy Gauge | Meet yourself where you are | Energy % + 1 line | Notice energy high/low |
| 2 | Ordinary Thanks | Notice what you usually take for granted | One line | Gratitude for familiar objects |
| 3 | Sonic Anchor | Listen to the moment | Short story | Sound that caught attention |
| 4 | Memory Portal | Visit a version of yourself | Paragraph | Detail bringing back past memory |
| 5 | Compassion Trigger | Catch kindness in the wild | Paragraph | Act of kindness noticed |
| 6 | Everyone Has a Universe | Everyone you pass is living a life as full as yours | Story | Imagined story of a stranger |
| 7 | One Percent | Get 1% closer to the person you want to become | One line | Embody 1 trait for 1 moment |
| 8 | Choose Your Own Adventure | One tiny act of courage | One line | Small step outside comfort zone |
| 9 | The Unspoken Word | Say the thing you almost didn't | One line / photo | Thought waiting to be said |
| 10 | Future Anchor | Leave a little space for "us" | One line | Discovery saved for future |
| 11 | Future Me | Send something forward | Paragraph | Message to self 1 year from now |

### 5.5 Photo Plate (Local Composer)

- Take a photo (camera) or choose from the library.
- Auto-compose a branded PNG card (1080px wide, Bodoni Moda + Josefin Sans).
- **Share** via Web Share API or **Save** as a download.
- No image ever leaves the device; there is no server upload.

### 5.6 Completion & Reflection Modal

- Shows an 11-cell calendar strip (`sq:log:v1`).
- Displays the quest's specific post-posting reflection quote when a day is completed.

---

## 6. Technical Constraints

| Item | Detail |
| --- | --- |
| Stack | Vanilla HTML, CSS, and JavaScript |
| Entry point | `index.html` + `manifest.json` + icon assets |
| Cycle start | `2026-09-10` (Thu 10/09/2026) |
| Storage | `localStorage` only |

---

## 7. Configuration Reference

Key constants in `index.html`:

```js
const START = new Date(2026, 8, 10);  // cycle start (Sept 10, 2026)
const WINDOW_OPEN  = 7;               // 7am
const WINDOW_CLOSE = 22;              // 10pm
```
