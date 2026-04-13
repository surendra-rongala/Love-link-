# 💕 Love Link — Phase 2 Complete

A production-ready mobile-first couple connection app built with React + Firebase.

---

## 🚀 Quick Start

### Frontend
```bash
cd frontend
npm install
npm run dev
```

### Backend (optional — only for push notifications)
```bash
cd backend
npm install
# Add serviceAccountKey.json from Firebase Console → Project Settings → Service Accounts
node server.js
```

---

## ⚙️ Firebase Setup

1. Create a project at [console.firebase.google.com](https://console.firebase.google.com)
2. Enable **Authentication → Anonymous**
3. Enable **Firestore Database**
4. Enable **Storage**
5. Copy your config into `frontend/src/lib/firebase.js`
6. Deploy Firestore rules: `firebase deploy --only firestore:rules`

---

## 🗂 Project Structure

```
love-link-final/
├── backend/
│   ├── server.js          # Express API — push notifications & cron jobs
│   ├── package.json
│   └── .env.example
├── frontend/
│   ├── src/
│   │   ├── pages/
│   │   │   ├── HomePage.jsx               ✅ Phase 1
│   │   │   ├── ChatPage.jsx               ✅ Phase 2 — gift trigger, ping, drafts
│   │   │   ├── GiftsPage.jsx              ✅ Phase 2 — unlockable, scheduled, voice
│   │   │   ├── MoodPage.jsx               ✅ Phase 1
│   │   │   ├── MemoryPage.jsx             ✅ Phase 1
│   │   │   ├── LoveNotesPage.jsx          ✅ Phase 1
│   │   │   ├── DatePlannerPage.jsx        ✅ Phase 1
│   │   │   ├── VibesPage.jsx              ✅ Phase 1
│   │   │   ├── LoveQuizPage.jsx           ✅ Phase 1
│   │   │   ├── BucketListPage.jsx         ✅ Phase 1
│   │   │   ├── LoveLetterPage.jsx         ✅ Phase 1
│   │   │   ├── RelationshipTrackerPage.jsx✅ Phase 1
│   │   │   ├── SettingsPage.jsx           ✅ Phase 1
│   │   │   ├── DailyConnectPage.jsx       🆕 Module 1 — Daily Question System
│   │   │   ├── InsightsPage.jsx           🆕 Module 4 — Relationship Insights
│   │   │   ├── AIAssistantPage.jsx        🆕 Module 8 — AI Love Coach (Claude API)
│   │   │   ├── PrivateSpacePage.jsx       🆕 Module 10 — PIN-protected private space
│   │   │   ├── OurStoryPage.jsx           🆕 — Relationship timeline/milestones
│   │   │   ├── LoveMissionsPage.jsx       🆕 — Daily challenges + badges
│   │   │   └── WeeklySummaryPage.jsx      🆕 — Auto-generated weekly love report
│   │   ├── components/
│   │   │   └── layout/
│   │   │       ├── AppShell.jsx           ✅ Updated — 20-item nav
│   │   │       ├── NotificationBanner.jsx
│   │   │       ├── LoadingScreen.jsx
│   │   │       └── ErrorBoundary.jsx
│   │   ├── lib/
│   │   │   ├── AuthContext.jsx
│   │   │   └── firebase.js               ← Add your config here
│   │   ├── hooks/
│   │   │   └── useDarkMode.js
│   │   └── styles/
│   │       └── globals.css
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
├── firestore.rules                        ✅ Phase 2 rules
└── storage.rules
```

---

## 🧩 Phase 2 Modules

| Module | Feature | Route |
|--------|---------|-------|
| 1 | Daily Connect — shared question, lock/unlock, streaks | `/daily` |
| 2 | Streak System — tracks daily activity, unlocks gifts | Firestore: `streaks/` |
| 3 | Smart Reminders — inactivity + mood alerts | Backend cron |
| 4 | Relationship Insights — chat graph, heatmap, AI tips | `/insights` |
| 5 | Dynamic Gift System — unlockable, scheduled, voice | `/gifts` |
| 6 | Live Presence — typing indicator, seen receipts | Chat (Firestore real-time) |
| 7 | Date Planner — mood-based suggestions, countdowns | `/dates` |
| 8 | AI Love Assistant — Claude-powered message coach | `/ai` |
| 9 | Account System — anonymous auth (upgrade path documented) | `/settings` |
| 10 | Push Notifications — smart triggers via backend | Backend |
| + | Private Space — PIN protected secrets & photos | `/private` |
| + | Our Story — relationship timeline + milestones | `/story` |
| + | Love Missions — daily challenges + badge system | `/missions` |
| + | Weekly Summary — auto love report + AI insight | `/summary` |
| + | Chat Enhancements — gift popup, thinking ping, drafts | `/chat` |

---

## 🔥 Firestore Collections

```
users/{uid}                        — user profiles, FCM tokens
couples/{coupleId}                 — couple data, moods, typing
  /messages/{msgId}                — chat messages
  /gifts/{giftId}                  — sent gifts
  /notes/{noteId}                  — love notes
  /daily_answers/{date}            — daily question answers (Phase 2)
  /drafts/{uid}                    — unsent chat drafts (Phase 2)
  /milestones/{id}                 — Our Story timeline (Phase 2)
  /private_{uid}/{docId}           — PIN-protected private space (Phase 2)
streaks/{coupleId}                 — streak counters (Phase 2)
missions/{coupleId_uid_date}       — daily mission completions (Phase 2)
mission_totals/{coupleId_uid}      — total points and badges (Phase 2)
```

---

## 🤖 AI Features (Claude API)

The app uses the Anthropic API directly from the browser for:
- **AI Love Assistant** (`/ai`) — relationship coaching, message suggestions, conflict help
- **Weekly Insight** (`/summary`) — personalized weekly love analysis

No API key setup needed — the Anthropic API is called through the claude.ai artifact proxy.

---

## 📲 Backend Push Notification Endpoints

| Endpoint | Trigger |
|----------|---------|
| `POST /notify-message` | New chat message |
| `POST /notify-gift` | Gift sent |
| `POST /notify-daily-question` | Daily question ready |
| `POST /notify-streak-warning` | Streak about to reset |
| `POST /notify-mood-alert` | Partner feeling sad |
| `POST /notify-inactive` | No chat in 24h |
| `GET /cron/daily-question` | Cron job — 9 AM daily |
| `GET /cron/check-inactive` | Cron job — every 6h |

---

## 💎 Unlockable Gift Tiers

| Tier | Unlock Condition |
|------|-----------------|
| Free Gifts | Always available |
| Premium Gifts 💎 | 7-day streak |
| Special Gifts 👑 | 30-day streak |

---

## 🛠 Tech Stack

- **React 18** + Vite
- **Firebase** (Auth, Firestore, Storage)
- **Tailwind CSS**
- **React Router v6**
- **date-fns** · **lucide-react** · **react-hot-toast**
- **Anthropic Claude API** (AI features)
- **Express.js** (backend)
