---
type: personal
tags: [notion, systems, life-os]
---
# Notion Deep Dive — Systems Map

*Extracted: March 1, 2026*

---

## LifeOS Architecture

The entire system lives under a single **LifeOS** page with two columns:

### Dashboard Column
- **Daily Command Center** — The daily hub. Shows: Current Objectives, Important Tasks, Training Log Daily, Food Log, Weekly Habits, Supplements.
- **Notes Database** — General notes.
- **Tasks Database** — All tasks, linked to Objectives.
- **Objetivos** — The goal system (see below).

### Personal Column
- **Strength & Recomp Tracker** — Body recomposition tracking (created Feb 2026).
- **Habitos** — 15 daily habit checkboxes.
- **Training Log** — Exercise tracking (exercise, reps/sets, form rating, date, notes).
- **Tabla de Calorias** — Food reference database (46 items with macros).
- **Suplementos** — 8 supplements tracked daily.
- **Mediciones** — Body measurements over time.
- **Finanzas** — Income/expenses + subscriptions.
- **Food Logs** — Food Log (individual meals) + Daily Macros (daily totals).

### Other Sections
- **Proyectos** — Project aliases.
- **Musica** — Rolas (songs).
- **NAHUAL** — Dedicated page.

---

## The Objective System

### Hierarchy
```
Vision + Mision (why)
  → Visiones Maestras (strategic pillars — max 5 active)
    → Objetivos (measurable goals — linked to a Master Vision)
      → Tasks (individual actionable tasks — linked to Objetivos)
```

### Philosophy (from the Objetivos page)
> "Solo podre trabajar en 5 al mismo tiempo. Estos objetivos son medibles y estan en mi control, son cosas que requieren de mi movimiento para hacerse, y no cosas abstractas como 'Ser feliz, etc'."

### Vision
> "Puedo moverme como un animal salvaje. Mi cuerpo es mi templo, mi arma y mi aliado."
> Music at will. Modern Da Vinci. Conscious philanthropy. Family in peace.
> **"Creo con proposito. Vibro en libertad. Y no fallo."**

### Mision
> "Expandir la conciencia. Superar los limites."

---

## 5 Master Visions (Active)

| Code | Name | Purpose | Status |
|------|------|---------|--------|
| **BBB** | Bring Back Bustos: Zenjaku | Web3 multidisciplinary artist. "Shaman web3." Fund consciousness projects. | 6/8 Done |
| **LVL-UP** | Level Up. Keep Learning Skills | Physical transformation. "Proyecto prioritario." Body as proof everything is possible. | 4/12 Done |
| **ART1** | Artist Flow State | Music production mastery. Ableton, mastering, recording, improv, content. | 0/3 Done |
| **GST** | Get Ship Together | Fix 3 years of accumulated mess. Clean ship = efficient navigation. | 3/9 Done |
| **GOOD** | (Baseline goals) | Recurring maintenance: environment, finances, security, health, growth, family, survival, fun. | 0/8 Done |
| **TN** | Templo Nahual | The app. (Page exists but is blank — no description written yet.) | - |

---

## Task System

Tasks are linked to Objetivos via a relation. Each task has:
- **Task ID** (title)
- **Task Name** (text)
- **Status**: Inbox → In Progress / Waiting → Done
- **Priority Zero** (checkbox for urgent tasks)
- **Objetivos** (relation to objectives)
- **Proyecto** (rollup from objective)
- **Master Vision** (rollup from objective)

The Tasks database has a **Focus Mode** view that filters to only show tasks linked to active objectives.

---

## Habits System (15 Daily Checkboxes)

| Habit | Category |
|-------|----------|
| Daily Journal | Reflection |
| Duolingo (Chinese) | Learning |
| Verduras (vegetables) | Nutrition |
| Practice / Created Music | Art |
| Daily Steps | Movement |
| Supplements | Health |
| 8 hours sleep | Recovery |
| No Fap | Discipline |
| Logged Stuff | Systems |
| Social Media Post | Output |
| Shower & Teeth | Self-care |
| Training | Fitness |
| Meditation | Mind |
| Flexibility & Mobility | Movement |
| Moisturize | Self-care |

---

## Food System

### Architecture
```
Tabla de Calorias (reference: 46 food items with macros per portion)
  → Food Log (individual meal entries — food item + portions + meal time)
    → Daily Macros (daily totals — calories, protein, carbs, fat via rollups)
```

### Meal Times
Desayuno, Comida, Cena, Snack, Pre-Train

### Macro Targets (from Recomp Tracker)
- Calories: 2,700 kcal
- Protein: 215g
- Carbs: 260g
- Fat: 78g

---

## Training Log

Each entry tracks:
- **Exercise** (64 options available)
- **Reps x Sets** (text)
- **Forma** (Perfect / Good / Mid / Bad)
- **Date**
- **Notes**
- **Objetivos Transformacion** (relation to objectives)

---

## Body Measurement System

Tracked in Mediciones database:
- Peso (kg)
- Grasa corporal (%)
- Musculo (%)
- Grasa Visceral (number)
- Notas

---

## Financial System

### Income / Expenses
Each entry: Tag, Name, Amount (MXN), Type (Gasto/Inversion/Ingreso/Suscripcion), Proyecto, Transaction Date, Notes, linked to Objetivos.

### Subscriptions
Active: YouTube Premium ($319/mo), Amazon Prime ($899/yr)
Inactive: Crunchyroll, Smartfit, Duolingo, Suno, Canva, Shaolin Online, Twitter, Dominio

---

## Key Relationships

```
Visiones Maestras
  ↓ (tagged via Master Vision select)
Objetivos
  ↓ (relation)          ↓ (relation)
Tasks              Ingresos/Gastos

Training Log → Objetivos (relation)
Food Log → Tabla de Calorias (relation) → Daily Macros (relation)
```

The system is well-designed for connecting daily actions to strategic goals. The chain runs: **Vision → Master Vision → Objetivo → Task → Daily execution**.
