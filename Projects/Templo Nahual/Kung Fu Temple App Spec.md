---
type: project
tags: [app, el-templo, tech-spec]
---
# Kung Fu Temple — Requirements & Tech Stack
_16 Jul 2025_

## Core Features

### 1. Home / Dashboard
- Daily goal progress (visual ring/bar)
- Streaks & XP tracking
- Motivational mascot (animated emoji/SVG)
- "Train Now" quick start

### 2. Stance Training
- Stance selector (cards with icons, descriptions, difficulty)
- Animated, tactile timer with sound/vibration
- Live feedback from mascot
- Celebration for new records

### 3. Progress & History
- Calendar view (heatmap or dots for training days)
- Charts (line/bar for best times, averages, XP)
- Session log (filterable by stance)

### 4. Gamification
- XP & levels (earn XP, level up, unlock stances/themes)
- Badges for streaks, milestones, personal bests
- Reminders (push notifications or in-app)

### 5. Customization
- Stance config (add/edit stances, set goals, choose icons)
- Themes (light/dark, color, mascot selection)

### 6. Mobile-First, PWA
- Installable (add to home screen, offline support)
- Touch-optimized, swipe navigation

---

## Tech Stack
- **Frontend:** React (with Vite or Next.js)
- **Styling:** Tailwind CSS (or Chakra UI, or custom CSS)
- **Routing:** React Router
- **State Management:** Zustand or Context API
- **Charts:** Chart.js or Recharts
- **Calendar/Heatmap:** react-calendar-heatmap or similar
- **Mascot Animations:** Lottie, animated SVG, or emoji
- **Persistence:** LocalStorage (or Firebase for cloud sync)
- **PWA:** Vite/Next.js PWA plugin

---

## Key Packages to Install
```sh
npm install react-router-dom zustand chart.js react-chartjs-2 react-calendar-heatmap
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

---

## Project Structure
```
src/
  components/
    Mascot.jsx
    StanceCard.jsx
    Timer.jsx
    ProgressChart.jsx
    CalendarHeatmap.jsx
    Badge.jsx
  pages/
    Home.jsx
    Train.jsx
    Progress.jsx
    Settings.jsx
  store/
    useStore.js
  stances.config.js
  App.jsx
  main.jsx
```

---

## Design/UX
- Duolingo-style: playful, colorful, animated, mobile-first
- Big touch targets, friendly mascot, confetti/celebration for wins
- Progress bars, streaks, and XP prominently displayed

---

## Vision Statement
_18 Jul 2025_

A transformation OS that combines physical, mental, and spiritual growth through structured, ritualistic skill trees, prioritizing authenticity and sovereignty over fleeting motivation.
