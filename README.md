# Japan AI/Data Career Map

A searchable, filterable reference platform for AI, Data, and Analytics roles in Japan. Built for candidates, recruiters, and hiring managers who want to understand the market clearly.

---

## Quick Start

```bash
npm install
npm run dev
```

Open `http://localhost:5173` in your browser.

---

## Build for Production

```bash
npm run build
```

Output goes to `dist/`. Deploy to any static host — Vercel, Netlify, GitHub Pages, or a standard CDN.

---

## Project Structure

```
src/
├── App.tsx                  # Root shell — navigation, dark mode
├── main.tsx                 # Entry point
├── index.css                # Tailwind base + CSS custom properties (theme)
│
├── types/
│   └── index.ts             # All TypeScript interfaces and types
│
├── utils/
│   └── index.ts             # Color maps, helper functions
│
├── hooks/
│   ├── useFilters.ts        # Filter state + URL serialization
│   └── useDarkMode.ts       # Dark mode with localStorage persistence
│
├── data/                    # ← Edit these to update content
│   ├── roles.json
│   ├── companies.json
│   ├── skills.json
│   ├── careerPaths.json
│   └── salaryRanges.json
│
├── components/
│   ├── Header.tsx
│   ├── FilterPanel.tsx
│   ├── RoleCard.tsx
│   └── CompareModal.tsx
│
└── pages/
    ├── RolesSection.tsx
    ├── CompaniesSection.tsx
    ├── SkillsSection.tsx
    ├── CareersSection.tsx
    ├── InterviewSection.tsx
    └── MarketSection.tsx
```

---

## How to Update the Data

All content lives in `src/data/`. JSON files are imported directly — no API or database needed.

### Adding or editing a role (`roles.json`)

Each role object requires these fields:

| Field | Type | Notes |
|---|---|---|
| `id` | string | Kebab-case, unique (e.g. `"data-analyst"`) |
| `title` | string | Display name |
| `titleJa` | string (optional) | Japanese title if relevant |
| `family` | string | One of: `Analytics`, `Data Engineering`, `ML/AI`, `Product`, `Consulting`, `Leadership` |
| `shortExplanation` | string | 1–2 sentence summary for cards |
| `whatTheyDo` | string | Paragraph-length description |
| `responsibilities` | string[] | Bullet-point list |
| `requiredSkills` | string[] | Must-haves |
| `niceToHaveSkills` | string[] | Good-to-haves |
| `tools` | string[] | Specific tools/platforms |
| `techFocus` | string[] | From the `TechFocus` union type |
| `japaneseLevel` | string[] | From the `JapaneseLevel` union type |
| `englishOnlyPossible` | boolean | Whether English-only candidates can apply |
| `seniority` | string[] | From the `Seniority` union type |
| `salary` | object | `{ junior, mid, senior, lead, note? }` |
| `companyTypes` | string[] | Free-text descriptions |
| `industries` | string[] | From the `Industry` union type |
| `workStyles` | string[] | From the `WorkStyle` union type |
| `interviewProcess` | object[] | `[{ stage, description }]` |
| `commonQuestions` | string[] | 4–6 questions |
| `careerProgression` | object[] | `[{ title, years, description }]` |
| `similarRoles` | string[] | Role IDs from this file |
| `recruiterNotes` | string | Internal/practical recruiting context |
| `commonMisconceptions` | string | What candidates/clients often get wrong |
| `demandLevel` | string | `High`, `Medium`, or `Low` |
| `remoteAvailability` | string | `Common`, `Possible`, or `Rare` |

### Adding a company (`companies.json`)

| Field | Type |
|---|---|
| `id` | string (kebab-case) |
| `name` | string |
| `nameJa` | string (optional) |
| `type` | string |
| `industry` | Industry[] |
| `size` | string |
| `rolesHiring` | string[] (role IDs) |
| `description` | string |
| `techStack` | string[] |
| `japaneseRequired` | boolean |
| `workStyle` | WorkStyle |
| `notable` | string |
| `website` | string (optional) |
| `headquarters` | string |

### Adding a skill (`skills.json`)

| Field | Type |
|---|---|
| `id` | string (kebab-case) |
| `name` | string |
| `category` | `Language` \| `Framework` \| `Cloud` \| `Tool` \| `Concept` \| `Soft Skill` |
| `description` | string |
| `relatedRoles` | string[] (role IDs) |
| `demandLevel` | `High` \| `Medium` \| `Low` |
| `learningPath` | string (optional) |

### Adding a career path (`careerPaths.json`)

| Field | Type |
|---|---|
| `id` | string (kebab-case) |
| `from` | string (role ID) |
| `to` | string (role ID) |
| `difficulty` | `Easy` \| `Moderate` \| `Challenging` |
| `timeframe` | string (e.g. `"1–2 years"`) |
| `description` | string |
| `bridgeSkills` | string[] |
| `notes` | string (recruiter perspective) |

### Updating salary benchmarks (`salaryRanges.json`)

Edit `benchmarks` for the salary table. Each entry: `{ role, junior, mid, senior, lead }`.
Edit `marketInsights` for the insight cards: `{ title, body }`.
Update `lastUpdated` to reflect when the data was refreshed.

---

## Features

- **Roles** — 20 AI/Data roles with full detail: responsibilities, skills, salary, interview process, career progression
- **Companies** — 15 companies hiring in Japan with tech stack and requirements
- **Skills Map** — 18 skills grouped by category with demand level and related roles
- **Career Transitions** — 10 common transition paths with difficulty, timeframe, and bridge skills
- **Interview Prep** — Questions and process stages per role, plus family-level prep tips
- **Market Notes** — Salary benchmarks, market insights, and hiring context for Japan
- **Dark mode** — System preference detected, persisted in localStorage
- **URL state** — Filters are serialized to URL search params for sharing
- **Role comparison** — Select up to 3 roles to compare side-by-side
- **Mobile responsive** — Works well on all screen sizes

---

## Tech Stack

- [React 18](https://react.dev/)
- [TypeScript 5](https://www.typescriptlang.org/)
- [Vite 5](https://vitejs.dev/)
- [Tailwind CSS 3](https://tailwindcss.com/)
- [Lucide React](https://lucide.dev/) — icons

No backend, no database. Everything is static JSON + client-side filtering.

---

## Deployment

### Vercel (recommended)

```bash
npm i -g vercel
vercel
```

### Netlify

Drag and drop the `dist/` folder into Netlify's dashboard, or connect the repo and set build command to `npm run build` with publish directory `dist`.

### GitHub Pages

Add `base: '/your-repo-name/'` to `vite.config.ts`, then build and push the `dist/` folder to the `gh-pages` branch.

---

## License

Internal tool. Not for redistribution without permission.
