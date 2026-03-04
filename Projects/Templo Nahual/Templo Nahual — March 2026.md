---
type: project
tags: [app, el-templo, features]
---
# Nahual Temple — App Features

**Platform:** React Native (Expo) — iOS, Android, Web
**Stack:** React 19, Zustand, Supabase, React Navigation

---

## Navigation

Four bottom tabs:

| Tab | Screen | Icon |
|-----|--------|------|
| Entrenar | Free Training | Barbell |
| Maestría | Guided Paths | Ribbon |
| Perfil | Profile & Stats | Person |
| Debug | Dev Tools (hidden) | — |

The Debug tab is revealed by triple-clicking the Profile tab.

---

## 1. Free Training ("Entrenar")

### Adding Exercises

Three-tab modal for adding exercises:

- **Exercises** — Search by name (ES/EN), filter by discipline or "Recent", grouped by discipline
- **Routines** — Preset routines (Fuerza Básica, Empuje y Tirón, Piernas y Core, Full Body Corto, Longevidad) and user-created custom routines
- **Goals** — Create personal targets (reps or time) per exercise, track progress

### Exercise Tracking

Four exercise types with dedicated UIs:

| Type | Input | Tracks |
|------|-------|--------|
| Reps | Numeric input | PR, streak, goal progress |
| Timer | Start/Pause/Stop + manual entry | Best time, countdown with vibration |
| Weighted | Weight (kg) + reps | Best weight, reps at best weight |
| Meditation | Timer-based | Duration |

All types support:
- Form evaluation (optional technique rating per attempt)
- Full attempt history with timestamps
- Expand to view history, edit or delete individual attempts (swipe)

### Exercise Management

- Add/remove exercises from active list
- Swipe-left to delete
- Mark exercises as favorites for quick access
- Daily reset clears selected exercises but preserves all history

### Streak Tracking

- Current streak (consecutive days) per exercise
- Best streak ever per exercise

### Custom Routines

- Create saved routines with specific exercises, sets, reps/time, and rest periods
- Launch as guided sessions with timed blocks and rest countdowns

---

## 2. Guided Masteries ("Maestría")

### Mastery Catalog

Structured training programs designed by experts, organized by category:

- Calistenia
- Movilidad
- Voz
- Artes Marciales

Each mastery includes: name, author, difficulty, description, frequency recommendation, and multiple phases.

### Mastery Structure

```
Mastery
 └─ Phase (2–5 per mastery)
     └─ Session
         └─ Block (Warmup → Main → Cooldown)
             └─ Exercise (sets, reps/time, rest, focus, cues)
```

Each phase has advancement criteria (qualitative and quantitative) that the user self-assesses.

### Guided Session Flow

1. Full-screen interface, one exercise at a time
2. Progress bar ("Exercise 2 of 8")
3. Block badges (Warmup/Main/Cooldown)
4. Timer with visual progress for timed exercises
5. Rest countdown between exercises (skippable)
6. Set tracking ("Set 1 of 3, each side")
7. Focus area and technique cues displayed per exercise
8. Complete / Skip / Exit controls

### Phase Progression

- User-driven advancement (not auto-unlock)
- Modal displays criteria checklist
- Can advance or regress to any phase
- Weekly consistency tracking (sessions per 7-day window)

### Pricing

- Free paths marked "GRATIS"
- Paid paths require authentication
- Beta mode overrides all prices (paths show "BETA", all free)

---

## 3. Profile ("Perfil")

### Calendar & History

- Monthly calendar highlighting training days
- Tap a day to see exercises completed, attempts, sets, and reps/time
- Exercise history expandable by month
- Per-exercise stats modal: all attempts, PR progression, streaks, frequency

### Authentication

Four sign-in methods:

| Method | Details |
|--------|---------|
| Email/Password | Sign up with display name, sign in |
| Google OAuth | via expo-auth-session |
| Apple OAuth | via expo-apple-authentication |
| Anonymous | Full app works without account |

Account prompt banner appears after 3 active days or 10 sessions (dismissible).

### Cloud Sync

Bidirectional merge with no data loss:

- **Trigger:** Manual (refresh button) or auto on app foreground
- **Strategy:** Union merge — keeps best of both local and cloud
  - Attempts deduplicated by timestamp
  - Streaks keep highest value
  - Sessions unioned across devices
- **Scope:** Exercise progress, active exercises, purchased paths, path progress, custom routines, custom goals, favorite exercises, user preferences

Sync status indicator and last-sync timestamp displayed in profile.

### Notification Settings

- Toggle daily reminders on/off
- Configurable reminder time (default 7 PM)
- 7 rotating motivational messages in Spanish
- Android notification channel support
- Permission request on first enable

### Other Settings

- Exercise language toggle (Spanish / English)
- Clear all local data (destructive, with confirmation)

---

## 4. Debug Screen (Hidden)

- **Mock date:** Set any date for testing, quick buttons (+1 day, +7 days)
- **Reset management:** View/clear last reset date, trigger manual daily reset
- **Data management:** Clear all data with confirmation
- **Beta mode:** Toggle free access to all masteries
- **Level unlock debug:** Skip phase advancement criteria

---

## 5. Exercise Catalog

### Data Sources (priority order)

1. **Remote:** Supabase `disciplines` + `exercises` tables
2. **Cached:** AsyncStorage (last synced version)
3. **Bundled:** `progressions.json` (5,440 lines, offline fallback)

### Catalog Sync

- `syncCatalog()` fetches from Supabase with 3-second timeout
- Falls back gracefully if offline
- Validates structure before caching

### Exercise Schema

```
id, name (ES), nameEn, type, target, nextTargets,
description (ES), descriptionEn, cues (ES), cuesEn,
image, videoUrl
```

### Disciplines

Calistenia, Movilidad, Voz, Artes Marciales, Meditación, and more.

---

## 6. Multi-Language Support

| Layer | Language |
|-------|----------|
| UI strings | Spanish (hardcoded) |
| Exercise names | Spanish or English (user toggle) |
| Onboarding | Bilingual options |
| Code/comments | English |

Exercise language is set during onboarding and changeable in Profile.

---

## 7. Data & Sync Architecture

### Supabase Tables

| Table | Purpose |
|-------|---------|
| `profiles` | Display name, timestamps (1:1 with auth.users) |
| `user_preferences` | Goals, level, disciplines, language, notifications |
| `exercise_progress` | Attempts, PR, streaks, completions per exercise |
| `active_exercises` | Currently tracked exercises |
| `purchased_paths` | Unlocked masteries |
| `path_progress` | Phase, sessions, last session per mastery |
| `custom_routines` | User-created routines |
| `custom_goals` | User-defined targets |
| `favorite_exercises` | Favorited exercise IDs |
| `disciplines` | Catalog: discipline metadata |
| `exercises` | Catalog: exercise metadata |

All user tables cascade on delete. JSONB fields for flexible nested data.

### State Management (Zustand)

| Store | Responsibility |
|-------|---------------|
| `appStore` | Mock date, language, tutorial, beta mode, preferences |
| `exerciseStore` | Active exercises, progress, attempts, streaks |
| `masteryStore` | Purchased paths, phase progress, session history |
| `authStore` | User, session, usage stats, sync timestamp |

### Offline-First Design

- Full app works without internet
- Sync queues operations and retries on foreground
- Catalog falls back to bundled JSON
- Auth is optional (anonymous usage fully supported)

---

## 8. Notifications

- Local push notifications (no remote server)
- Daily training reminder at configurable time
- Streak-at-risk alerts
- Weekly training summary
- 7 rotating motivational messages
- Android channel setup, iOS system dialog
- Settings persisted to AsyncStorage and synced to Supabase

---

## 9. UI & Design System

### Color Palette

- **Background:** Dark grays (#060608, #0D0D12) with blue undertone
- **Primary accent:** Gold (#D4AF37) with glow variants
- **Text:** White (#F5F5F7), gray variants
- **Status:** Green, Red, Purple, Blue

### Key Components

- `Button`, `Card`, `SearchBar`, `FilterButtons`, `ModalHeader`
- `ActiveExerciseView` — full exercise tracking UI
- `ExerciseSelectorModal` — exercise picker with search/filter
- `GuidedSessionModal` — step-by-step session execution
- `RoutineCreatorModal`, `CreateGoalModal`
- `TutorialModal` — 4-step onboarding flow
- `AuthModal` — login/signup interface
- `AccountPromptBanner` — smart account creation prompt
- `DayViewModal`, `ExerciseStatsModal` — profile statistics

### Interactions

- Swipe gestures (delete exercises/attempts)
- Pulse animations on save
- Linear gradients for depth
- BlurView modal overlays

---

## 10. Onboarding (TutorialModal)

Four-step flow:

1. **Welcome** — App introduction
2. **Goals** — Select training goals (bilingual options)
3. **Experience** — Beginner / Intermediate / Advanced
4. **Disciplines** — Choose exercise categories

Exercise language selection included. Preferences saved locally and synced to cloud.

---

## 11. Hooks & Utilities

| Module | Purpose |
|--------|---------|
| `useGuidedSession()` | Manages guided session state, timers, progression for both routines and masteries |
| `useTimer()` | Timer with pause/resume and manual input |
| `exerciseUtils.js` | Catalog lookup, search, filtering, name formatting |
| `timeUtils.js` | Time formatting (MM:SS, readable, parsing) |
| `dataManager.js` | Catalog initialization, attempt logging |
| `notifications.js` | Permission, scheduling, settings persistence |
| `syncService.js` | Bidirectional cloud sync with merge logic |
