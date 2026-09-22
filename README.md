# CareerOS 🛰️
### Your Personal IT Career Operating System

CareerOS is an interactive, animated career-intelligence experience for working IT professionals. Instead of a static form-and-dashboard, it turns your role, experience, skills, and goals into a living map — showing where you stand today, which career paths fit you, what skills to build next, and a concrete 90-day plan to get there.

**🔗 Live demo:** `https://<your-username>.github.io/careeros/` *(enable GitHub Pages — see below)*

---

## ✨ What it does

| Feature | Description |
|---|---|
| **Cinematic Hero** | A mouse-reactive constellation of IT career nodes, connected by animated glowing paths. |
| **Interactive Onboarding** | One question at a time — role, experience (animated slider), skills (chip selection), and goal. |
| **Career Identity** | An animated readiness ring, current/emerging strengths, and opportunity areas based on your profile. |
| **Career Universe** | The centerpiece — your current role sits at the center of a constellation of possible paths, connected by strength-weighted lines. Click a node to zoom into a full fit analysis. |
| **Learn Next Bridge** | An animated skill bridge from where you are to your target role, with click-to-expand explanations for each skill. |
| **Skill Gap Visualizer** | A radial, category-based map of what you know, what's recommended next, and what comes later. |
| **Compare Paths** | Side-by-side comparison of up to 3 career paths — alignment, gap, complexity, and a suggested first project. |
| **90-Day Roadmap** | A scroll-revealing, three-phase learning plan with milestones. |
| **What-If Simulator** | Toggle a skill you don't have yet and watch every career path's match score recalculate live. |
| **AI Career Coach** | Ask a career question, get a structured answer (recommendation, why, what you have, what to learn, first action) — built as a deterministic demo engine, structured so a real LLM API can be dropped in later. |

---

## 🧱 Tech Stack

CareerOS is intentionally shipped as a **single self-contained `index.html`** — no build step, no `npm install` required to run it.

- **React 18** — via CDN (UMD build)
- **Babel Standalone** — in-browser JSX transpilation
- **Vanilla CSS** — custom design system (glassmorphism, glow, CSS keyframe animation, SVG-driven visuals)
- **No external UI framework** — all charts, constellations, rings, and roadmaps are hand-built with SVG + CSS for full control over the "career OS" aesthetic

This makes the project trivially portable: clone it, open it, done.

---

## 🎨 Design Direction

- Deep navy / near-black background with electric blue + controlled purple accents
- Glassmorphic translucent panels, thin borders, soft glow
- Subtle background grid, layered depth, generous negative space
- Motion used meaningfully (state changes, hierarchy, progress) — not decoration
- Full `prefers-reduced-motion` support

---

## 🚀 Getting Started (VS Code)

### Run locally — no installs required
1. Clone the repo:
   ```bash
   git clone https://github.com/<your-username>/careeros.git
   cd careeros
   ```
2. Open the folder in VS Code.
3. Right-click `index.html` → **Open with Live Server** (install the *Live Server* extension by Ritwick Dey if you don't have it)
   — or just double-click `index.html` to open it directly in your browser.

That's it. React, Babel, and fonts load from CDN at runtime.

### Try the demo profile
On the hero screen, click **"Load Demo Profile"** in the top-right corner to instantly load a pre-built profile:

- **Role:** Software Developer
- **Experience:** 3 years
- **Skills:** React, JavaScript, Git, AWS
- **Goal:** Move Into DevOps

---

## 🌐 Deploy with GitHub Pages

1. Go to your repo → **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: `main`, folder: `/ (root)` → **Save**
4. Visit `https://<your-username>.github.io/careeros/` after ~1 minute

---

## 📂 Project Structure

```
careeros/
├── index.html      # Entire application — markup, styles, and React app
└── README.md
```

Everything — data model, scoring engine, UI components, and screens — lives inside `index.html`, organized into clearly labeled sections:

```
DATA            → roles, skills, goals, career paths, skill explanations
ENGINE          → path scoring, readiness calculation, strength analysis
UI PRIMITIVES   → ProgressRing, useInView hook
NAVBAR
SCREENS         → Hero, Onboarding, BuildingSequence, CareerIdentity,
                   CareerUniverse, LearnNext, SkillGapVisualizer,
                   ComparePaths, Roadmap90, WhatIfSimulator
AI CAREER COACH → deterministic response engine + chat UI
APP ROOT        → state management + screen routing
```

---

## 🧠 How the recommendation engine works

CareerOS doesn't call an external API — it uses a transparent, rule-based scoring model:

- Each career path defines **core skills** (defining) and **required skills** (full learning path)
- A user's match score weights core-skill overlap (70%) and required-skill overlap (30%)
- Skill gaps are split into **Learn Next** (top 3 missing) and **Learn Later** (the rest)
- Readiness score blends skill count, years of experience, and goal clarity

This logic lives in the `ENGINE` section of `index.html` and is fully deterministic — the same inputs always produce the same outputs, which makes the app predictable, debuggable, and easy to extend.

---

## 🔮 Extending CareerOS

- **Swap in a real AI backend:** replace `generateCoachResponse()` with a call to an LLM API (e.g. the Anthropic API) — the input/output shape (recommendation, why, have, learnNext, firstAction) is already structured for this.
- **Add more roles/paths:** extend `CAREER_PATHS` and `SKILL_GROUPS` in the `DATA` section.
- **Persist profiles:** currently state is in-memory only (resets on refresh) — add `localStorage` if you want profiles to persist between visits.

---

## ⚠️ Disclaimer

CareerOS provides skill-alignment guidance based on a self-reported profile. It does **not** predict guaranteed salaries or employment outcomes — treat it as a career exploration tool, not a promise.

---

## 📄 License

MIT — free to use, modify, and build on.
