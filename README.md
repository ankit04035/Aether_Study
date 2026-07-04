# 📚 AetherStudy — Smart Study Planner & Productivity Hub

<div align="center">

![StudyMentor Banner](https://img.shields.io/badge/StudyMentor-Productivity%20Hub-8b5cf6?style=for-the-badge&logo=book&logoColor=white)
![Version](https://img.shields.io/badge/version-1.0.0-06b6d4?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-10b981?style=for-the-badge)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

**A premium, all-in-one study management application featuring Task Planning, Pomodoro Timer, Flashcard Decks with Spaced Repetition, Custom Quiz Maker, and Active Recall Reminders.**

[🌐 Live Demo](#) · [📖 Documentation](#detailed-guide) · [🚀 Quick Start](#quick-start) · [🤝 Contributing](#contributing)

</div>

---

## 📋 Table of Contents

- [✨ Features Overview](#-features-overview)
- [🛠️ Tech Stack](#️-tech-stack)
- [📁 Project Structure](#-project-structure)
- [🚀 Quick Start](#-quick-start)
- [🔄 Application Workflow](#-application-workflow)
- [🗺️ Flow Diagrams](#️-flow-diagrams)
- [📖 Detailed Module Guide](#-detailed-module-guide)
- [💾 Data Persistence](#-data-persistence)
- [🎨 Design System](#-design-system)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## ✨ Features Overview

| Module | Description |
|--------|-------------|
| 🏠 **Dashboard** | Central overview of focus stats, active tasks, reminders and Pomodoro widget |
| ✅ **Task Manager** | Create tasks with priority tags, estimated Pomodoro cycles, categories |
| ⏱️ **Pomodoro Timer** | SVG animated ring timer with Work / Break / Long Break modes |
| 🃏 **Flashcard Decks** | 3D animated card flipping with Easy / Medium / Hard spaced repetition |
| 📝 **Quiz Maker** | Build custom multiple-choice quizzes and take interactive tests |
| 🔔 **Active Recall Reminders** | Schedule pop-up alerts that require answering a quiz question to dismiss |

---

## 🛠️ Tech Stack

```
Frontend:      HTML5, CSS3 (Custom Properties, Grid, Flexbox, Animations)
JavaScript:    Vanilla ES6+ (Modules, LocalStorage, Web Audio API)
Design:        Glassmorphism, CSS 3D Transforms, SVG Animations
No frameworks, no dependencies — runs in any modern browser
```

---

## 📁 Project Structure

```
studymentor/
│
├── index.html          # Main SPA shell with all 6 tab views & modal templates
├── style.css           # Design system: variables, layout, components, animations
├── app.js              # Core orchestrator: state, router, theme, Web Audio chimes
├── tasks.js            # Task board: create, filter, complete, delete tasks
├── pomodoro.js         # Timer controller: ticking, SVG ring progress, sound
├── flashcards.js       # Deck manager: 3D flip, spaced repetition (SRS) scoring
├── quiz.js             # Quiz builder: create, take, score, review results
├── reminders.js        # Reminder scheduler: interval timers, active recall modal
└── README.md           # This documentation file
```

---

## 🚀 Quick Start

### Prerequisites

- Any modern browser (Chrome 90+, Firefox 88+, Edge 90+, Safari 14+)
- Python (for local dev server) or any static file server

### Run Locally

```bash
# Clone the repository
git clone https://github.com/ankit04035/studymentor.git
cd studymentor

# Option 1: Python 3
python -m http.server 8000

# Option 2: Python 2
python -m SimpleHTTPServer 8000

# Option 3: Node.js live-server
npx live-server

# Open in browser
# http://localhost:8000
```

> ⚠️ **Important**: Do NOT open `index.html` directly as a file (`file://`) — always use a local server to ensure scripts load correctly.

---

## 🔄 Application Workflow

### High-Level User Journey

```
┌─────────────────────────────────────────────────────────────────────┐
│                         StudyMentor App                             │
│                                                                     │
│   User Opens App → Dashboard loads with Stats & Widgets            │
│          │                                                          │
│          ▼                                                          │
│   ┌──────────────┐   ┌──────────────┐   ┌──────────────────────┐   │
│   │  Add Tasks   │   │  Set Timer   │   │  Create Flashcards   │   │
│   │  with Tags & │──▶│  Link Task   │   │  & Study Decks       │   │
│   │  Priorities  │   │  and Focus   │   │                      │   │
│   └──────────────┘   └──────────────┘   └──────────────────────┘   │
│          │                  │                      │                │
│          ▼                  ▼                      ▼                │
│   ┌──────────────┐   ┌──────────────┐   ┌──────────────────────┐   │
│   │  Filter &    │   │  Pomodoro    │   │  3D Flip Cards       │   │
│   │  Complete    │   │  Session     │   │  Rate: Easy/Med/Hard │   │
│   │  Tasks       │   │  Stats Saved │   │  (Spaced Repetition) │   │
│   └──────────────┘   └──────────────┘   └──────────────────────┘   │
│                                                                     │
│   ┌──────────────┐   ┌──────────────────────────────────────────┐   │
│   │  Build Quiz  │──▶│  Set Active Recall Reminder (interval)   │   │
│   │  (MCQ)       │   │  ↓ Timer fires → Quiz modal pops up      │   │
│   └──────────────┘   │  ↓ Answer correct → Reminder dismissed   │   │
│                       │  ↓ Wrong answer → Retry or Snooze       │   │
│                       └──────────────────────────────────────────┘   │
│                                                                     │
│   All data auto-saved to localStorage → persists on refresh         │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 🗺️ Flow Diagrams

### 1. Task Management Flow

```
START
  │
  ▼
[Fill Task Form]
  ├── Title
  ├── Category (Study / Exam / Homework / Reading / Project)
  ├── Priority (Low / Medium / High)
  └── Estimated Pomodoros (1–10)
  │
  ▼
[Add Task to Board]
  │
  ├──▶ Active Tasks Column
  │         │
  │         ├── [🍅 Log Pomodoro] ──▶ Increment completed count
  │         ├── [✅ Complete]     ──▶ Move to Completed Column
  │         └── [🗑️ Delete]       ──▶ Remove from state
  │
  └──▶ Completed Tasks Column
            │
            └── [⏪ Re-Activate] ──▶ Move back to Active
  │
  ▼
[State saved to localStorage]
  │
  ▼
[Dashboard Stats Updated]
END
```

### 2. Pomodoro Timer Flow

```
START
  │
  ▼
[Select Mode]
  ├── Work Session    (default 25 min)
  ├── Short Break     (default 5 min)
  └── Long Break      (default 15 min)
  │
  ▼
[Optional: Link to Active Task]
  │
  ▼
[Press ▶ Start]
  │
  ├── SVG ring animates (stroke-dashoffset decreasing)
  ├── Time displayed in center
  ├── Nav bar shows "Focusing: MM:SS"
  └── Web Audio API chime plays (ascending chord)
  │
  ▼
[Timer Running]
  │
  ├── [Pause] ──▶ Timer pauses, icon switches to ▶
  ├── [Reset] ──▶ Returns to full duration, stopped
  └── [Completes]
          │
          ├── Alarm chime plays (3-pulse)
          ├── Focus minutes added to stats
          ├── Linked task Pomodoro count incremented
          └── Auto-switch to Break mode
  │
  ▼
[Stats Updated → localStorage]
END
```

### 3. Flashcard Spaced Repetition Flow

```
START
  │
  ▼
[Create Deck]
  │
  ▼
[Add Cards] ──▶ Front (Term/Question) + Back (Definition/Answer)
  │
  ▼
[Click Deck to Study]
  │
  ▼
[Cards sorted by difficulty]
  ├── 🔴 Hard  → shown first
  ├── 🆕 New   → shown second
  ├── 🟡 Medium → shown third
  └── 🟢 Easy  → shown last
  │
  ▼
[View Front Side]
  │
  ▼
[Click Card / "Show Answer"] ──▶ 3D flip animation
  │
  ▼
[View Back Side]
  │
  ▼
[Rate your memory]
  ├── 🟢 Easy   ──▶ card.difficulty = "easy"   → pushed to end next session
  ├── 🟡 Medium ──▶ card.difficulty = "medium" → middle priority
  └── 🔴 Hard   ──▶ card.difficulty = "hard"   → first next session
  │
  ▼
[Next Card] ──▶ Repeat until all done
  │
  ▼
[Session Complete] ──▶ Success chime + stats updated
END
```

### 4. Quiz Maker Flow

```
START
  │
  ▼
[Create Quiz]
  ├── Quiz Title
  ├── Category
  └── Add Questions (1 or more):
          ├── Question text
          ├── Option A, B, C, D
          └── Select correct answer (radio button)
  │
  ▼
[Publish Quiz] ──▶ Saved to state
  │
  ▼
[Click Quiz Card to Play]
  │
  ▼
[Question displayed]
  │
  ▼
[User selects option]
  ├── ✅ Correct ──▶ Green highlight, +1 score, success chime
  └── ❌ Wrong   ──▶ Red highlight, correct shown in green, fail buzz
  │
  ▼
[Next Question] ──▶ Repeat per question
  │
  ▼
[Quiz Complete]
  ├── Score ratio shown (e.g., 3/5)
  ├── Percentage shown (e.g., 60%)
  ├── Encourage message based on score
  ├── Wrong answers listed for review
  └── Score saved to quiz history (affects Dashboard avg)
END
```

### 5. Active Recall Reminder Flow

```
START
  │
  ▼
[Create Reminder]
  ├── Title
  ├── Source Quiz (random question drawn from this)
  ├── Interval (number)
  └── Unit (Seconds / Minutes / Hours)
  │
  ▼
[Reminder Activated] ──▶ setInterval() starts ticking
  │
  ▼ (after interval elapses)
[Modal Overlay Appears] ──▶ Alarm chime plays
  │
  ├── Shows title
  ├── Random question from selected quiz
  └── 4 multiple choice answers
  │
  ▼
[User selects answer]
  ├── ✅ Correct ──▶ Modal closes after 1.2s
  │                   ──▶ Bell chime plays
  └── ❌ Wrong   ──▶ Correct answer shown
                     ──▶ Modal stays for 2.5s then closes
                     ──▶ Fail buzz plays
  │
  OR
  │
  ▼
[User clicks Snooze] ──▶ Re-triggers after 2 minutes
  │
  ▼
[Reminder repeats on next interval]
END
```

### 6. Data Persistence Flow

```
User Action
    │
    ▼
State mutated in AetherState (in-memory JS object)
    │
    ▼
saveState() called
    │
    ▼
State serialized → JSON.stringify()
    │
    ▼
Stored in localStorage key: "AETHER_STUDY_STATE"
    │
    ▼
Page Refresh / Re-open
    │
    ▼
loadState() reads localStorage
    │
    ▼
State parsed → JSON.parse()
    │
    ▼
All modules re-render from restored state
    │
    ▼
Reminder timers re-initialized from saved reminders
```

---

## 📖 Detailed Module Guide

### 🏠 Dashboard (`app.js`)

The Dashboard serves as the command center with four key stat cards:

| Stat Card | Data Source | Updates When |
|-----------|-------------|--------------|
| **Focus Minutes** | `pomodoro.stats.focusMinutes` | Work cycle completes |
| **Tasks Done** | `tasks.filter(completed)` | Task marked complete |
| **Cards Reviewed** | `flashcards.reviewedCount` | Card rated in study session |
| **Avg Quiz Score** | `quizHistory` average | Quiz completed |

**Quick Widgets:**
- **Pomodoro widget**: Mirrors timer state — controls are synced with the full Pomodoro page
- **Focus Tasks widget**: Top 3 active tasks preview
- **Reminders widget**: Top 3 active reminders preview

---

### ✅ Task Manager (`tasks.js`)

**Creating a Task:**
```
Input: Title, Category Tag, Priority, Estimated Pomodoros
Output: Task card added to Active column with color-coded priority stripe
```

**Priority Color System:**
- 🔴 `High` → Red left border
- 🟣 `Medium` → Purple left border  
- ⚫ `Low` → Gray left border

**Category Tags:**
```
📚 Study  |  📝 Exam Prep  |  ✏️ Homework  |  📖 Reading  |  💻 Project  |  🌟 Other
```

**Pomodoro Progress Indicators:**
- Each estimated Pomodoro is shown as a 🍅 tomato icon
- Completed Pomodoros are full-opacity; remaining are 25% opacity
- Clicking ➕ on a task manually logs one Pomodoro cycle

---

### ⏱️ Pomodoro Timer (`pomodoro.js`)

**Timer Modes:**

| Mode | Default | Ring Color |
|------|---------|------------|
| Work Session | 25 min | Violet (#8b5cf6) |
| Short Break | 5 min | Cyan (#06b6d4) |
| Long Break | 15 min | Cyan (#06b6d4) |

**Technical Implementation:**
- Uses `Date.now()` timestamps instead of pure `setInterval` counting — this prevents timer drift when the browser tab is backgrounded or throttled
- SVG circle uses `stroke-dashoffset` calculated as: `circumference × (1 - timeLeft/maxDuration)`
- Web Audio API synthesizes chimes without any external audio file dependencies

**Custom Durations:**
You can override all three durations in the "Duration Rules" card. Changes take effect immediately and are persisted in localStorage.

---

### 🃏 Flashcard Decks (`flashcards.js`)

**Spaced Repetition Algorithm:**

Cards are sorted before each session based on their `difficulty` property:

```javascript
const difficultyOrder = { 'hard': 1, 'new': 2, 'medium': 3, 'easy': 4 };
cards.sort((a, b) => difficultyOrder[a.difficulty] - difficultyOrder[b.difficulty]);
```

This ensures:
- 🔴 **Hard** cards are reviewed first and most frequently
- 🆕 **New** cards get high priority
- 🟡 **Medium** cards come after new
- 🟢 **Easy** cards appear at the end

**3D Card Flip CSS Architecture:**
```css
.flashcard-3d-wrapper       → perspective: 1000px
  .flashcard-inner          → transform-style: preserve-3d; transition: rotateY
    .flashcard-front        → shown by default
    .flashcard-back         → transform: rotateY(180deg); backface-visibility: hidden
```

Adding class `.flipped` to wrapper triggers the 180° rotation.

---

### 📝 Quiz Maker (`quiz.js`)

**Building a Quiz:**
1. Enter Quiz Title and Category
2. Click **"+ Add Question"** to add question panels
3. For each question:
   - Enter the question text
   - Fill in Options A, B, C, D
   - Select the correct answer using the radio button
4. Click **"Publish Quiz"**

**Taking a Quiz:**
- Progress bar advances with each question
- Options lock after answering (no changing answers)
- Correct answer highlighted green, wrong highlighted red
- "Next Question" appears after each answer

**Scoring Grades:**

| Score | Message |
|-------|---------|
| 100% | 🏆 Flawless victory! |
| 80–99% | 🌟 Fantastic effort! |
| 50–79% | 📖 Good effort! Review errors. |
| < 50% | 📚 Keep going! Review corrections. |

---

### 🔔 Active Recall Reminders (`reminders.js`)

This is the most unique feature of StudyMentor. Rather than a passive notification, reminders actively test your knowledge.

**How it works:**
1. You schedule a reminder linked to a Quiz source
2. After the set interval, a full-screen overlay appears
3. A random question from the linked quiz is drawn
4. You **must answer correctly** to dismiss the overlay
5. Wrong answers show the correct answer but eventually auto-dismiss
6. Snooze re-triggers in 2 minutes (or 5 seconds in testing mode)

**Interval Units:**

| Unit | Recommended Use |
|------|----------------|
| Seconds | Testing / development |
| Minutes | During study sessions (e.g., every 30 min) |
| Hours | Scheduled daily review (e.g., every 2 hours) |

---

## 💾 Data Persistence

All data is stored in your browser's `localStorage` under the key `AETHER_STUDY_STATE`.

**Stored Data Shape:**
```json
{
  "theme": "dark",
  "tasks": [...],
  "pomodoro": {
    "durationWork": 25,
    "durationShortBreak": 5,
    "durationLongBreak": 15,
    "linkedTaskId": null,
    "soundEnabled": true,
    "stats": { "focusMinutes": 120 }
  },
  "flashcards": {
    "decks": [...],
    "reviewedCount": 42
  },
  "quizzes": [...],
  "quizHistory": [...],
  "reminders": [...]
}
```

> **Note:** Data is stored locally in your browser. It does NOT sync across devices. Clearing browser data will reset the app to defaults.

---

## 🎨 Design System

StudyMentor uses a **CSS Custom Properties** based design system with dark/light theme support.

**Color Palette (Dark Mode):**
```css
--bg-dark:      #0f111a    /* Page background */
--bg-card:      rgba(26, 29, 46, 0.45)  /* Glassmorphic cards */
--primary:      #8b5cf6    /* Neon Violet — primary actions */
--secondary:    #06b6d4    /* Cyan — break modes & links */
--accent:       #f43f5e    /* Coral Rose — alerts & warnings */
--text-main:    #f8fafc    /* Primary text */
--text-muted:   #94a3b8    /* Subdued text */
```

**Category Color System:**
```css
Study:    #8b5cf6  (violet)
Exam:     #f43f5e  (coral)
Homework: #3b82f6  (blue)
Reading:  #10b981  (emerald)
Project:  #f59e0b  (amber)
Other:    #64748b  (slate)
```

**Glassmorphism Cards:**
```css
background: rgba(26, 29, 46, 0.45);
backdrop-filter: blur(16px);
border: 1px solid rgba(255, 255, 255, 0.08);
border-radius: 18px;
```

---

## 🤝 Contributing

Contributions are welcome! Here's how to get started:

1. **Fork** the repository
2. **Clone** your fork:
   ```bash
   git clone https://github.com/YOUR_USERNAME/studymentor.git
   ```
3. **Create a branch**:
   ```bash
   git checkout -b feature/your-feature-name
   ```
4. **Make your changes** and commit:
   ```bash
   git add .
   git commit -m "feat: add your feature description"
   ```
5. **Push** to your fork:
   ```bash
   git push origin feature/your-feature-name
   ```
6. Open a **Pull Request**

### Contribution Ideas
- [ ] Add drag-and-drop task ordering
- [ ] Export quiz results as PDF
- [ ] Import/export deck data as JSON
- [ ] Add dark/light theme persistence
- [ ] Add a calendar/schedule view
- [ ] Add streak tracking for study sessions
- [ ] Mobile app wrapper (PWA)

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

```
MIT License — Copyright (c) 2026 Ankit

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files, to deal in the Software
without restriction, including without limitation the rights to use, copy,
modify, merge, publish, distribute, sublicense, and/or sell copies of the
Software.
```

---

<div align="center">

**Made with ❤️ for focused learners everywhere**

[![GitHub](https://img.shields.io/badge/GitHub-ankit04035-181717?style=flat-square&logo=github)](https://github.com/ankit04035)

</div>
