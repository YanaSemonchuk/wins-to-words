# Wins-to-Words 🧪→📝

> A personal pet project: turn small weekly work wins into LinkedIn posts and an always-up-to-date CV, without waiting for inspiration.

**Status:** Phase 1 (no-code MVP) · **Owner:** @YanaSemonchuk · **Type:** learning sandbox, not a commercial product

---

## 1. Problem

As a career switcher (organic chemistry → IT PM → scientific software PM), I:
- postpone updating my CV because collecting achievements from memory is slow and painful;
- rarely post on LinkedIn because "I don't know what to write about".

**Root-cause hypothesis:** the problem isn't writing, it's having no raw material. Wins aren't captured when they happen, so every post or CV update starts from a blank page.

## 2. Goal

Build a lightweight system where **10 minutes a week** of capturing wins is enough to produce:
- 3+ post ideas per month,
- CV bullets ready for the next application.

Secondary goal: learn GitHub (issues, milestones, PRs, Actions) and AI-agent basics hands-on.

## 3. Jobs to be done

1. **When** I do something valuable at work or in learning, **I want to** log it in under 1 minute, **so that** I don't lose it.
2. **When** I want to post, **I want** 3–5 topics from my real experience, **so that** I don't depend on inspiration.
3. **When** a dream role (ELN/LIMS, cheminformatics, drug discovery tooling) appears, **I want** a tailored CV in 30 minutes, **so that** I don't miss the window.

## 4. Approach: phased build

| Phase | What | Tech | Learns | Milestone |
|---|---|---|---|---|
| **1. No-code MVP** | Markdown templates + prompts used with Claude | Markdown only | Repos, commits, issues, milestones | `v0.1` |
| **2. Script** | Python script reads `wins/` and generates post ideas + CV bullets | Python + Claude API | Branches, PRs, `.env`/secrets, README docs | `v0.2` |
| **3. Agent** | Scheduled GitHub Action opens a monthly issue with post topics | GitHub Actions + Claude API | CI/CD, automation, agent design | `v0.3` |

Each phase only starts if the previous one proved useful (see success metrics).

## 5. Scope: Phase 1 (MVP)

### In scope
- `templates/weekly-win.md`: weekly capture template (3 questions, 10 min)
- `prompts/post-ideas.md`: wins → 3–5 post topics with hooks
- `prompts/cv-bullets.md`: wins → STAR / impact-style CV bullets
- `prompts/career-bridge.md`: map chemistry/lab experience → PM / scientific software value
- `cv/master-cv.md`: master CV kept in Markdown
- Friday reminder (calendar, outside repo)

### Out of scope (non-goals)
- Auto-posting to LinkedIn (API limits + risk to the account; posting stays manual)
- UI / web app
- Multi-user support
- Analytics on post performance

## 6. User stories & acceptance criteria

**US-1: Capture a win**
As a PM, I want a short weekly template so that I can log wins quickly.
- AC1: Template has ≤ 3 questions (Did / Learned / Impact).
- AC2: Filling it takes ≤ 10 min.
- AC3: File naming `wins/YYYY-Www.md` sorts chronologically.

**US-2: Generate post ideas**
As a PM, I want to turn the last 4 weeks of wins into post topics so that I always have something to post.
- AC1: Prompt returns 3–5 topics, each with a hook line and a target audience.
- AC2: At least 1 topic connects to the scientific software / career-switch angle.
- AC3: Output contains no names or internal figures.

**US-3: Generate CV bullets**
As a PM, I want CV bullets from my wins so that my CV stays current.
- AC1: Each bullet follows "action + result + metric (if available)".
- AC2: Bullets are appended to `cv/master-cv.md` under the right role.

**US-4: Bridge my background**
As a career switcher, I want my lab experience reframed in PM terms so that recruiters in scientific software see the fit.
- AC1: Prompt outputs 3–5 statements mapping lab skills → PM/product skills.

### Edge cases
- A week with "nothing happened" → template still asks for 1 learning (no empty weeks).
- A win is internal-only by design: describe the action and outcome, not names or figures ("streamlined the project-start registry process").
- Missed 2+ weeks → monthly catch-up prompt instead of guilt.

## 7. Repo structure (Phase 1)

```
wins-to-words/
├── README.md
├── templates/
│   └── weekly-win.md
├── prompts/
│   ├── post-ideas.md
│   ├── cv-bullets.md
│   └── career-bridge.md
├── cv/
│   └── master-cv.md
├── wins/                     # internal cases, no names or data
└── .gitignore
```

## 8. Backlog (GitHub issues)

| # | Issue | Label | Milestone |
|---|---|---|---|
| 1 | Create repo + README + `.gitignore` | `setup` | v0.1 |
| 2 | Add "no names, no data" checklist to `weekly-win.md` | `template` | v0.1 |
| 3 | Write `weekly-win.md` template | `template` | v0.1 |
| 4 | Write `post-ideas.md` prompt | `prompt` | v0.1 |
| 5 | Write `cv-bullets.md` prompt | `prompt` | v0.1 |
| 6 | Write `career-bridge.md` prompt | `prompt` | v0.1 |
| 7 | Run 4-week experiment + retro | `experiment` | v0.1 |
| 8 | Python script: read `wins/` → call Claude API | `feature` | v0.2 |
| 9 | Monthly GitHub Action → opens issue with post topics | `feature` | v0.3 |

## 9. Success metrics (4-week experiment)

| Metric | Target |
|---|---|
| Weeks with a logged win | 4 / 4 |
| Post ideas generated | ≥ 6 |
| Posts actually published | ≥ 2 |
| Time from idea to published post | ≤ 30 min |
| CV updated with new bullets | Yes |

**Go / no-go for Phase 2:** at least 3/4 weeks logged and 2 posts published.

## 10. Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Discipline drops after week 2 | High | 10-min Friday calendar slot; catch-up prompt |
| Internal company details slip into a public repo | Low | Wins are internal cases written without names or data by design; quick re-read before each commit |
| Posts sound "AI-generated" | Medium | Prompts produce topics + hooks; I write the text myself |
| Claude API costs (Phase 2+) | Low | Monthly runs only; set a spend limit |
| Scope creep (UI, auto-posting) | Medium | Non-goals list above |

## 11. Open questions

- Post language: EN, UA, or both?
- Main purpose of posts: recruiter visibility in scientific software, networking, or a general personal brand?
