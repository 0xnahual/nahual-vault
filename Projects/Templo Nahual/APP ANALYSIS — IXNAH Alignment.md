---
type: project
tags: [app, el-templo, IXNAH, analysis]
---
# [[Kung Fu Temple App Spec|El Templo]] App — [[What is IXNAH|IXNAH]] Alignment Analysis

*What needs to change, what stays, and why.*

---

## The Core Problem

The app is currently a **general fitness tracker that happens to include IXNAH content.** It needs to become **an IXNAH system tracker that happens to have great tracking tools.**

The difference is not cosmetic. It's architectural. Right now the app says "bring any exercise, we'll track it." It should say "this is the IXNAH system. Here's how you train it."

---

## What's Already Perfect (Don't Touch)

These features are exactly right for an IXNAH app. They stay as-is:

| Feature | Why It's Right |
|---------|---------------|
| **Timer exercise type** | Stances are timed holds. Breathing spells are timed protocols. This is IXNAH's core tracking mechanic. |
| **Meditation exercise type** | Breathing spells (Hechiceria del Aliento) are meditation-adjacent. The timer-based tracking fits perfectly. |
| **Streak tracking** | IXNAH is a daily practice. Current + best streak per exercise is the right gamification. |
| **Calendar heatmap** | Visual proof of consistency. Directly supports the IXNAH philosophy of daily practice. |
| **Mastery system structure** | Phase → Session → Block → Exercise is exactly how IXNAH is structured (9 Stages, progressions, protocols). This is the app's best feature. |
| **Phase progression (user-driven)** | IXNAH mastery tests are self-assessed. Auto-unlock would be wrong. User decides when they've earned it. |
| **Guided session flow** | Full-screen, one exercise at a time, progress bar, rest countdowns — this is exactly how IXNAH protocols should be delivered. |
| **Offline-first design** | People train in gyms, parks, dojos — often without signal. Critical. |
| **Anonymous usage** | Let people train first, create account later. Removes friction. Smart. |
| **Account prompt after 3 days / 10 sessions** | Proves value before asking for commitment. Keep. |
| **Dark UI with gold accent** | Looks like a temple. Matches the brand. Don't change. |
| **Cloud sync (bidirectional merge)** | Union merge with no data loss is the right strategy. Keep. |
| **Daily reset clears selection but preserves history** | Clean daily slate, permanent record. Right behavior. |
| **Form evaluation (technique rating)** | Self-assessment of form is exactly how IXNAH mastery works. Keep. |
| **PR tracking** | "Best time" for stances, "best streak" — these are IXNAH mastery milestones. |
| **Bilingual exercise names (ES/EN toggle)** | Your vault says "Spanish first, translate for reach." Having both is perfect. |
| **PWA / React Native (Expo)** | Cross-platform, installable, offline. Right tech for the product. |

---

## What Needs to Change

### 1. The Exercise Catalog — The Biggest Change

**Current state:** `progressions.json` has 5,440 lines. That's hundreds of exercises across generic fitness categories. The app syncs from Supabase with disciplines like "Calistenia, Movilidad, Voz, Artes Marciales, Meditacion, and more."

**Problem:** You're maintaining a massive exercise database of movements you don't do, haven't vetted, and can't vouch for. This is the exact thing we decided against. Every exercise in El Templo should be something YOU have done, tested, and can explain with authority.

**What to do:**

Strip the catalog down to IXNAH exercises only. Here's the complete list based on the IXNAH Compendium and your vault:

**Discipline: Posturas (7 exercises) — FREE TIER**
| Exercise | Type | Mastery Test |
|----------|------|-------------|
| Ma Bu (Horse Stance) | Timer | 2 min at parallel, calm breathing |
| Gong Bu (Forward Stance) | Timer | Unilateral stability, clean transitions |
| Pu Bu (Drop Stance) | Timer | Controlled descent and rise, both sides |
| Asian Squat (Deep Squat) | Timer | 5 min comfortable, heels flat |
| Dead Hang | Timer | 60 sec passive, controlled breathing |
| Tree Pose | Timer | 60 sec each side, eyes closed |
| Forward Fold | Timer | Palms flat on floor, relaxed breathing |

**Discipline: Fuerza — Empuje / Push (8 exercises)**
| Exercise | Type |
|----------|------|
| Wall Pushup | Reps |
| Incline Pushup | Reps |
| Standard Pushup | Reps |
| Deficit Pushup | Reps |
| Diamond Pushup | Reps |
| Explosive Pushup | Reps |
| Pike Pushup | Reps |
| Handstand Hold | Timer |

**Discipline: Fuerza — Tiron / Pull (7 exercises)**
| Exercise | Type |
|----------|------|
| Body Row / Australian Pullup | Reps |
| Pullup | Reps |
| Weighted Pullup | Weighted |
| Gi/Towel Pullup | Reps |
| Muscle-up | Reps |
| Dead Hang (active) | Timer |

**Discipline: Fuerza — Dips & Press (4 exercises)**
| Exercise | Type |
|----------|------|
| Bench Dip | Reps |
| Parallel Bar Dip | Reps |
| Weighted Dip | Weighted |
| Ring Dip | Reps |

**Discipline: Fuerza — Skill (5 exercises)**
| Exercise | Type |
|----------|------|
| L-sit Hold | Timer |
| Front Lever Hold | Timer |
| Planche Lean | Timer |
| Handstand Hold | Timer |
| Pistol Squat | Reps |

**Discipline: Fuerza — Lower Body (4 exercises)**
| Exercise | Type |
|----------|------|
| Bodyweight Squat | Reps |
| Bulgarian Split Squat | Reps |
| Cossack Squat | Reps |
| Pistol Squat | Reps |

**Discipline: Movilidad / Mobility (8 exercises)**
| Exercise | Type |
|----------|------|
| Hip CARs | Reps |
| 90/90 Hip Switch | Reps |
| Pigeon Hold | Timer |
| Jefferson Curl | Reps |
| Cat/Cow | Reps |
| Thoracic Rotation | Reps |
| Wall Angels | Reps |
| Ankle Dorsiflexion Stretch | Timer |

**Discipline: Respiracion / Breathing Spells (6 exercises)**
| Exercise | Type |
|----------|------|
| Pulso del Jaguar (Box Breathing) | Meditation |
| Hechizo de Wim Hof | Meditation |
| Viento Silencioso (4-7-8) | Meditation |
| Tiempo en Equilibrio (Square) | Meditation |
| Luna Silenciosa (Left Nostril) | Meditation |
| Rayo Interior (Holotropic) | Meditation |

**Discipline: Artes Marciales (when you're ready — can add over time)**
| Exercise | Type |
|----------|------|
| Heavy Bag Rounds | Timer |
| Shadowboxing | Timer |
| Uchikomi (Throw Entries) | Timer |
| Jump Rope | Timer |

**Discipline: Voz / Voice (keep if content exists)**
| Exercise | Type |
|----------|------|
| Whatever voice exercises you have documented | Timer/Reps |

**Total: ~55-60 exercises.** Not 500. Every single one vetted by you.

**What happens to the 5,440-line `progressions.json`:** Archive it. Create a new one with only IXNAH exercises. The Supabase tables get the same treatment — only IXNAH exercises in the database.

---

### 2. Navigation — Rename and Reframe

**Current:**
| Tab | Screen | Icon |
|-----|--------|------|
| Entrenar | Free Training | **Barbell** |
| Maestria | Guided Paths | Ribbon |
| Perfil | Profile & Stats | Person |

**Problems:**
- **"Entrenar" with a barbell icon** signals "gym tracker." IXNAH is not a gym. The barbell icon is literally the symbol of the thing you're moving AWAY from.
- **"Free Training"** implies unstructured gym work. IXNAH has structure even in free sessions.
- **"Maestria" / "Guided Paths"** is generic. These are IXNAH mastery paths, not random expert programs.

**Suggested:**
| Tab | Screen | Icon Suggestion |
|-----|--------|------|
| **Entrenar** | Daily Practice | Flame, temple gate, or fist — anything that says "training" without saying "gym" |
| **Camino** | IXNAH Paths | Path/road, mountain, or the current ribbon is fine |
| **Perfil** | Profile & Stats | Person (keep) |

The key change is the icon. The barbell has to go. It tells every new user "this is another gym app." A flame, a temple gate, a fist, or even a simple circle/zen symbol would immediately signal "this is something different."

---

### 3. The "Weighted" Exercise Type — Keep But Limit

**Current:** Weight (kg) + reps tracking. Tracks best weight and reps at best weight.

**Concern:** This is the gym tracker mechanic. But — and this is important — IXNAH does include weighted calisthenics (weighted pullups, weighted dips). These ARE IXNAH exercises.

**Decision:** Keep the Weighted type, but it only appears for the specific IXNAH exercises that use it (weighted pullup, weighted dip, and maybe deadlift/farmer's walk if you add those to IXNAH later). Since the exercise catalog is curated, this resolves itself — the Weighted type exists but only for IXNAH exercises that need it.

No changes needed to the tracking UI. The curation of the catalog is the fix.

---

### 4. Preset Routines — Replace with IXNAH Programs

**Current presets:** Fuerza Basica, Empuje y Tiron, Piernas y Core, Full Body Corto, Longevidad.

**Problem:** These are generic calisthenics routines. "Empuje y Tiron" (Push and Pull) is gym programming language. None of these reference IXNAH.

**Replace with IXNAH-specific routines:**

| Routine Name | Contents | Duration |
|-------------|----------|----------|
| **Las 7 Posturas** | All 7 Medicine Postures, progressive holds | 20-30 min |
| **Postura Rapida** | 3 postures (Ma Bu + Dead Hang + Asian Squat), short holds | 10 min |
| **Fuerza del Nahual** | Pushup + Pullup + Dip + Pistol Squat progressions | 30-40 min |
| **Hechiceria del Aliento** | 3 breathing spells in sequence (pre-training or post-training) | 15-20 min |
| **Guerrero Completo** | Postures + Strength + Breathing (full IXNAH session) | 45-60 min |
| **Movilidad Sagrada** | 4 Sacred Mobility Portals (Hip, Hamstring, Thoracic, Ankle) | 20-30 min |
| **Modo Guerrero** | Wim Hof breathing + Explosive warmup + Heavy bag rounds | 25-35 min |
| **Modo Mistico** | 4-7-8 breathing + Slow postures + Forward Fold | 20-25 min |

These routines are the IXNAH system in session format. A user picks one and gets a guided IXNAH experience, not a generic workout.

**Custom routines:** Keep the feature. Users should be able to build their own sessions from the curated exercise list. But the PRESETS should be IXNAH programs.

---

### 5. Mastery Catalog — Rebrand from "Designed by Experts"

**Current:** "Structured training programs designed by experts."

**Problem:** Who are these experts? This is YOUR system. Saying "designed by experts" sounds like you hired trainers to create content. That's what every fitness app says. The whole point of IXNAH is that it comes from YOUR transformation, YOUR training, YOUR system.

**Change to:** "The IXNAH system" or "IXNAH Training Paths" or "By Ricardo Bustos / 0xnahual."

Each mastery path's author field should say **"IXNAH"** or **"0xnahual"** — not "expert." You are the author. Own it.

**Current categories:** Calistenia, Movilidad, Voz, Artes Marciales.

**Suggested categories for mastery paths:**

| Category | What It Contains |
|----------|-----------------|
| **Fundacion** | 7 Medicine Postures mastery path (the free entry point) |
| **Fuerza** | Calisthenics progression paths (push, pull, skill) |
| **Movilidad** | 4 Sacred Portals path |
| **Respiracion** | 6 Breathing Spells mastery |
| **Sistema Nervioso** | Warrior Mode / Mystic Mode protocols |
| **Combate** | Heavy bag, shadowboxing, martial arts basics (when ready) |
| **Voz** | Voice training (if content exists) |

These categories map directly to the IXNAH Compendium's structure. The app becomes a digital version of the book.

---

### 6. Disciplines — Align with IXNAH Domains

**Current disciplines in Supabase:** Calistenia, Movilidad, Voz, Artes Marciales, Meditacion, "and more."

**Problem:** "And more" is the red flag. What else is in there? If it's not IXNAH, it shouldn't exist in the database.

**Replace with IXNAH-aligned disciplines:**

| Discipline | Maps to IXNAH |
|-----------|---------------|
| **Posturas** | Part 1: Foundation — 7 Medicine Postures |
| **Movilidad** | Part 1: Foundation — 4 Sacred Mobility Portals |
| **Fuerza** | Part 2: Strength — Calisthenics progressions |
| **Respiracion** | Part 5: Nervous System — 6 Breathing Spells |
| **Combate** | Part 3: Combat — Heavy bag, shadowboxing, martial arts |
| **Voz** | Separate discipline (your unique addition to the system) |

No "Meditacion" as a separate discipline — breathing spells ARE the meditation layer, filed under Respiracion. No "Calistenia" as generic — it becomes "Fuerza" within the IXNAH system.

---

### 7. Onboarding — Reframe for IXNAH

**Current 4-step flow:**
1. Welcome — App introduction
2. Goals — Select training goals (bilingual)
3. Experience — Beginner / Intermediate / Advanced
4. Disciplines — Choose exercise categories

**Problems:**
- "Select training goals" is generic fitness app language
- "Choose exercise categories" implies a buffet. IXNAH is a system, not a buffet.
- Experience levels (Beginner/Intermediate/Advanced) don't map to IXNAH's 9 Stages

**Suggested flow:**

1. **Welcome** — "This is El Templo. The IXNAH training system." Brief, branded, sets the tone.
2. **Where are you?** — Instead of generic experience levels, ask IXNAH-relevant questions:
   - "Can you hold Ma Bu for 30 seconds?" → determines starting point
   - "Do you train martial arts?" → shows/hides combat content
   - "Have you done breathwork before?" → determines breathing spell starting point
   - Or simpler: "Starting from zero" / "I move well but want structure" / "I already train and want to track"
3. **Language** — Spanish or English (keep)
4. **Start** — Drop them into the 7 Postures as their first path. No category selection. Everyone starts at the foundation. This IS the IXNAH philosophy: "You start at Part 1 no matter who you are — the foundation is not optional."

The onboarding should feel like entering a dojo, not configuring a fitness app.

---

### 8. Exercise Schema — Minor Adjustments

**Current:**
```
id, name (ES), nameEn, type, target, nextTargets,
description (ES), descriptionEn, cues (ES), cuesEn,
image, videoUrl
```

**Issues:**
- `target` and `nextTargets` — These are muscle group fields ("chest," "back," "legs"). IXNAH doesn't think in muscle groups. IXNAH thinks in capabilities (Moving, Strength, Violence, Defending, Longevity) and body systems (joints, nervous system, posterior chain).

**Suggested change:**
- Rename `target` → `domain` — Maps to IXNAH capability: "Foundation", "Strength", "Combat", "Breathing", "Mobility"
- Rename `nextTargets` → `progressesTo` — What exercise comes next in the IXNAH skill tree (e.g., Wall Pushup → Incline Pushup → Standard Pushup)
- Add field: `masteryTest` — Short description of what mastery looks like for this exercise
- Add field: `medicine` — What this exercise heals/develops (unique to IXNAH: "confidence under load", "spinal decompression", "posterior chain lengthening")

The `image` and `videoUrl` fields are fine — you can add media when you create it. Leave them nullable.

---

### 9. Goals Feature — Reframe as Mastery Tests

**Current:** "Create personal targets (reps or time) per exercise, track progress."

**This is actually great for IXNAH.** The mastery tests ARE goals:
- Ma Bu: goal = 2 minutes
- Dead Hang: goal = 60 seconds
- Pushups: goal = 20 strict reps
- Pullups: goal = 5 strict reps

**Suggestion:** Pre-populate goals with IXNAH mastery tests for each exercise. User can still create custom goals, but the default goals ARE the IXNAH standards. When a user hits a mastery test goal, celebrate it as a milestone — not just "goal achieved" but "Ma Bu Mastery Unlocked" or "Postura del Guardian: Dominada."

This turns the generic goals feature into an IXNAH achievement system with zero code changes — just data.

---

### 10. Notifications — Reframe Language

**Current:** "7 rotating motivational messages in Spanish."

**Suggestion:** Make these IXNAH-themed. Pull from the 9 Pillars, the Presence Code, your best aphorisms. Examples:
- "Atencion: donde miras, creas." (Pillar 1)
- "El cuerpo lidera. La consciencia sigue." (IXNAH core principle)
- "Las posturas no construyen guerreros. Construyen humanos que pueden moverse." (IXNAH definition)
- "Presencia es habitar el cuerpo, el momento, la consciencia." (Pillar 7)
- "No hay atajo. Hay practica." (Your vault, multiple sources)

This is a tiny change but it makes every notification feel like the app is part of the system, not a generic fitness reminder.

---

## What to REMOVE

| Feature/Content | Why Remove |
|----------------|-----------|
| Any exercise not in IXNAH | You can't vouch for it. It dilutes the brand. |
| Generic discipline categories ("and more") | IXNAH has specific domains. No "and more." |
| Generic preset routines (Empuje y Tiron, etc.) | Replace with IXNAH-named programs |
| "Designed by experts" copy | You are the author. Own it. |
| Barbell icon | It signals gym. IXNAH is not a gym. |
| The bulk of progressions.json (5,440 lines) | Archive. New file with ~55-60 IXNAH exercises. |
| Muscle-group-based fields (target, nextTargets) | Replace with IXNAH domain + progression chain |

---

## What to ADD

| Feature/Content | Why Add | Priority |
|----------------|---------|----------|
| **Pre-populated mastery tests as default goals** | Turns generic goals into IXNAH achievement system | High — data only, no code |
| **IXNAH-branded preset routines** (Las 7 Posturas, Guerrero Completo, etc.) | Replaces generic routines with system sessions | High — data only, no code |
| **Nervous System Mode Toggle** | Your vault describes Warrior Mode vs Mystic Mode. Could be a session modifier: "Train in Warrior Mode" (intense, timed, competitive) vs "Train in Mystic Mode" (slow, meditative, recovery). Changes the timer sounds, colors, or pace. | Medium — minor UI + logic |
| **9 Stages progress indicator** | Show the user where they are on the IXNAH journey. Based on accumulated mastery across disciplines. Not a game mechanic — a mirror. | Medium — needs design |
| **"What this heals" text per exercise** | Each IXNAH exercise is medicine for something specific. Show it. Ma Bu: "confidence under load." Dead Hang: "spinal decompression." This is what makes the app feel like IXNAH, not a tracker. | High — data only |
| **Capable Human Checklist** | A single screen showing all IXNAH mastery standards and which ones the user has passed. The "finish line" (that's never really finished). From Chapter 23 of the Compendium. | Medium — new screen |

---

## The Transition Plan — How to Do This Without Rewriting the App

This is mostly a **data migration, not a code rewrite.** The app's architecture is solid. The tracking engine, timer, streak system, mastery flow, sync, auth — all stay. What changes is the CONTENT inside the app and some labels.

### Phase 1: Data (can be done in days, not weeks)
1. Create new `progressions-ixnah.json` with ~55-60 curated exercises
2. Update Supabase `disciplines` table with IXNAH-aligned categories
3. Update Supabase `exercises` table — remove non-IXNAH exercises
4. Create IXNAH preset routines in the routines table/data
5. Pre-populate mastery test goals for each exercise
6. Add "medicine" / "what this heals" descriptions to each exercise

### Phase 2: UI Labels (can be done in hours)
1. Change barbell icon to something IXNAH-branded
2. Update "Designed by experts" → "The IXNAH System" / "by 0xnahual"
3. Update notification messages with IXNAH aphorisms
4. Update onboarding copy
5. Rename preset routines

### Phase 3: Schema (minor, can be done with Phase 1)
1. Rename `target` → `domain` in exercise schema
2. Rename `nextTargets` → `progressesTo`
3. Add `masteryTest` and `medicine` fields
4. Migrate existing data

### Phase 4: New Features (post-launch, premium)
1. Nervous System Mode Toggle
2. 9 Stages progress indicator
3. Capable Human Checklist screen
4. IXNAH-branded onboarding flow

**The critical insight: Phase 1 and 2 are the entire transformation.** The app already has the right engine. It just has the wrong fuel in it. Swap the exercises, swap the labels, and you have an IXNAH app — without rewriting a single tracking feature.

---

## The Final Picture

**Before (current):**
> A general fitness tracker with timer, reps, and weighted tracking. 500+ exercises across generic categories. Preset routines named after gym splits. "Designed by experts." Barbell icon. Could be any fitness app.

**After (IXNAH-aligned):**
> The IXNAH training system in your pocket. 55-60 curated exercises across Postures, Strength, Mobility, Breathing, Combat, and Voice. Each exercise has a mastery test and a description of what it heals. Preset sessions named after the system (Las 7 Posturas, Guerrero Completo, Modo Mistico). Mastery paths authored by you. The 7 Medicine Postures are free. Everything else is premium. No exercise exists in this app that its creator hasn't done.

That last sentence is the moat. No other fitness app can say that. Every other app has a database of exercises scraped from somewhere. El Templo has a system forged in the 127 → 89 arc, curated by the person who lived it.

---

## One Thing to Watch Out For

You'll be tempted to add exercises "just in case" or "because people might want them." This is the slippery slope back to a general tracker. The rule is simple:

**If it's in the IXNAH Compendium, it's in the app. If it's not, it's not.**

When you start training deadlifts consistently and they earn a place in the Compendium, add them to the app. When you develop the combat layer through judo and boxing and the protocols are documented, add them. The app grows as the system grows. Never ahead of it.

The app is the system. The system is the app. Nothing more, nothing less.
