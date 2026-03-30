# claude-quant-resume-skill ⚔️📄

> 🎯 A fully ATS-optimized, human-sounding resume — projects pulled from your GitHub, experience from LinkedIn, keywords extracted from the JD, and a 3-pass internal review already done.
>
> 🪶 **Zero dependencies, zero lock-in.** The entire system is plain Markdown files. One `SKILL.md` readable by any Claude-compatible agent. Fork it, adapt it, make it yours.
>
> *💡 This is a methodology, not a platform. The resume workflow is what matters — take it anywhere. 🌱*

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Compatible with: Claude.ai](https://img.shields.io/badge/Claude.ai-Skills-blueviolet)](https://claude.ai)
[![ATS Target Score: 95+](https://img.shields.io/badge/ATS%20Score-95%2B-brightgreen)]()
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-orange.svg)](CONTRIBUTING.md)
[![agentskills.io](https://img.shields.io/badge/agentskills.io-standard-blue)](https://agentskills.io)

[🚀 Quick Start](#-quick-start) · [🔍 GitHub + LinkedIn Extraction](#-github--linkedin-extraction) · [📈 3-Pass Review Loop](#-3-pass-review-loop) · [🏦 Target Companies](#-target-companies) · [🤝 Contributing](#-contributing)

> ⭐ If this helped you land an interview, star the repo — it helps others find it.

---

## 🎯 More Than Just a Resume Builder

**Basic mode** — share your GitHub + LinkedIn, get a resume:
```
"Write me an ATS resume for a quant researcher role at Citadel.
 My GitHub: github.com/username
 My LinkedIn: [paste Experience + Education text]"
```
Claude scans your repos, scores them against the role, merges with LinkedIn experience, and builds your resume — using only what you actually built.

**🔥 JD-Mirror mode** — paste the actual job posting:
```
"Here's the Jane Street QR job posting: [paste JD]
 My GitHub: github.com/username
 My LinkedIn: [paste profile text]"
```
Claude reads the JD → scores your repos against its keywords → selects the most relevant projects → rewires every bullet to match the JD's exact phrasing.

**🔥 Score mode** — audit an existing resume:
```
"Score my resume against quant ATS standards: [paste resume]"
```

---

## 🔍 GitHub + LinkedIn Extraction

This is what makes this skill unique. Instead of asking you to describe your projects from scratch, Claude pulls them directly from where they already live.

### GitHub

Claude fetches your public repos via the GitHub API (no token needed), scores each one against the JD, and shows you a relevance scan before writing a single line:

```
REPO RELEVANCE SCAN
====================
Repo: pairs-trading-strategy      Score: 9/10  ✅ INCLUDE
  Matches JD: Python, backtesting, equity, statistical arbitrage
  Tech found: Python, pandas, statsmodels, matplotlib
  Metric in README: "1.4 Sharpe ratio in out-of-sample backtest"

Repo: monte-carlo-pricer          Score: 8/10  ✅ INCLUDE
  Matches JD: C++, options pricing, Monte Carlo, derivatives
  Metric in README: "50k contracts/sec on synthetic order flow"

Repo: personal-website            Score: 1/10  ⛔ SKIP
Repo: advent-of-code-2023         Score: 2/10  ⛔ SKIP
```

Only repos scoring ≥ 5 make it into the resume. Metrics are only used if they appear in YOUR README — never fabricated.

**What Claude extracts from each repo:**

| Source | What's extracted |
|--------|-----------------|
| Repo description | Project name + what it does |
| README (first 150 lines) | What it does, metrics, outcomes |
| `requirements.txt` / `package.json` / `CMakeLists.txt` | Tech stack (Python, C++, etc.) |
| Repo topics + language | Additional tech stack signals |
| Last commit date | Approximate project completion date |

**Resulting bullet:**
```
Implemented a pairs-trading strategy in Python (pandas, statsmodels) using
Engle-Granger cointegration on 5 years of equity tick data, achieving 1.4 Sharpe
in out-of-sample backtests
```
Every word in that bullet came from your repo. Nothing invented.

### LinkedIn

LinkedIn blocks automated scraping, so Claude supports three input methods:

| Method | How | Best for |
|--------|-----|---------|
| **Paste text** | Copy-paste your Experience + Education sections | Fastest — 30 seconds |
| **Upload PDF** | LinkedIn → Settings → Get a copy of your data → Profile PDF → upload | Most complete |
| **Public URL** | Share your profile URL — Claude attempts `web_fetch` | Works on public profiles; falls back to paste if blocked |

**What Claude extracts:**

- Exact job titles (never upgraded — "intern" stays "intern")
- Companies, dates (converted to `Month YYYY – Month YYYY`)
- Responsibilities (rewritten as Action Verb → Task → Result, never copied verbatim)
- Education, GPA (only if ≥ 3.5), relevant coursework
- Skills, certifications (CFA, FRM, CQF, Coursera, etc.)

### GitHub + LinkedIn merged

When both are provided, Claude cross-references them:

```
LinkedIn says:  "Built ML pipeline for trade signal generation" at Firm X
GitHub has:     repo trade-signal-ml → XGBoost, Python, README shows 54% accuracy

Merged bullet:
"Built an XGBoost trade-signal ML pipeline in Python (scikit-learn, pandas) at Firm X,
 achieving 54% directional accuracy on 18 months of equity data"
```

Not fabrication — both sources confirm the same work. The merge makes it specific.

### If neither is available

Claude asks for everything in one structured message — no back-and-forth required.

---

## 📈 3-Pass Review Loop

Every resume goes through three internal passes **before any output is produced**.

| Pass | What it checks | What it fixes |
|------|---------------|---------------|
| **① ATS Gate** | Keywords, date format, section headers, banned phrases, fabrication check | Hard formatting and keyword failures |
| **② Human Voice Check** | Passive voice, identical bullet rhythm, AI filler words, vague bullets | Rewrites to sound specific and human-authored |
| **③ Hiring Manager Scan** | Strongest line on page 1, logical narrative arc, skills match bullets | Restructures flow, removes noise |

If any pass fails → revise → re-run all 3 passes. Only then does output happen.

**Before / after Pass 2:**

| ❌ Before | ✅ After |
|-----------|---------|
| "Responsible for data analysis in a fast-paced environment" | "Analyzed 3 years of order-book tick data in Python, identifying a mean-reversion signal with 0.42 Sharpe across 12 equity pairs" |
| "Helped develop ML models for trading" | "Built an XGBoost price-direction classifier on 18 months of 1-min OHLCV data, achieving 54.2% directional accuracy vs 50.8% baseline" |
| "Good communication skills, team player" | *(deleted — replaced with a concrete bullet)* |

---

## 🚀 Quick Start

### Option 1: Claude.ai Skills UI
```
1. Download quant-resume-writer.skill from Releases
2. Claude.ai → Settings → Skills → Upload Skill
3. Start a new chat and say:
   "Write me a quant resume. My GitHub: github.com/username"
```

### Option 2: Claude Code / API
```bash
git clone https://github.com/pooja2420/claude-quant-resume-skill.git
cp -r claude-quant-resume-skill/skills/quant-resume-writer ~/.claude/skills/
claude
```

### Option 3: Manual
Upload `skills/quant-resume-writer/SKILL.md` directly as a skill file or system prompt.

---

## 🧩 Four Modes

| Mode | Trigger | Use when | ATS lift |
|------|---------|----------|---------|
| `WRITE` | "write my resume" + GitHub/LinkedIn | Starting from scratch | Baseline |
| `OPTIMIZE` | "improve my resume" + paste | Existing resume needs work | +15–25 pts |
| `JD-MIRROR` | Paste a job description | Tailoring to one specific role | +25–40 pts |
| `SCORE` | "score my resume" | Auditing without rewriting | — (report only) |

> 💡 **Auto-detection:** Paste a JD → JD-Mirror activates. Share a GitHub URL → repo extraction activates. No need to specify modes.

---

## 🏦 Target Companies

**Quant Firms**

| Company | ATS Platform | What they look for |
|---------|-------------|-------------------|
| Citadel | Lever | Math olympiad, Putnam, top GPA, research. Human-first after basic filter |
| Jane Street | Internal | Probability, expected value, game theory. Résumé is a conversation starter |
| IMC Trading | Greenhouse | Derivatives, options pricing, C++. Online test is the real filter |
| Two Sigma / DE Shaw | Greenhouse | ML, alternative data, factor models. Research papers valued |
| Nasdaq | iCIMS | Financial data, real-time systems, domain knowledge |

**Big Tech**

| Company | ATS Platform | Key quirk |
|---------|-------------|-----------|
| Amazon | Workday | Hard keyword match — exact phrase matters |
| Google | gHire | GPA and school weighted. Algorithmic problem-solving |
| Meta | Greenhouse | PyTorch, open-source ML. GitHub links scanned |
| Microsoft | Workday | Breadth valued. Azure, ML, system design |
| Apple | Workday | On-device ML, efficiency, privacy-preserving ML |
| Netflix | Lever | Experimentation at scale, A/B testing |
| Walmart / CVS | Workday / Taleo | Supply chain / health analytics. Taleo strips all formatting |

> ⚠️ **Workday**: `Month YYYY – Month YYYY` date format only — no slashes, no ordinals.
> ⚠️ **Taleo** (CVS): No special characters, no icons in section headers.

---

## 🔄 Full Workflow

```
User shares GitHub URL + LinkedIn + (optional) JD
              │
              ▼
  ┌───────────────────────────────────┐
  │  Step 0: Profile Extraction       │
  │  ① Fetch GitHub repos via API    │
  │  ② Score repos against JD/role   │
  │  ③ Extract LinkedIn experience   │
  │  ④ Cross-reference & merge       │
  │  ⑤ Ask only for missing gaps     │
  └───────────────────────────────────┘
              │
              ▼
  ┌───────────────────────────────────┐
  │  Mode Detection                   │
  │  WRITE / OPTIMIZE / JD-MIRROR     │
  └───────────────────────────────────┘
              │
    ┌─────────┴──────────┐
    ▼                    ▼
[JD provided]       [No JD]
Extract keywords    Use role defaults
Build match report
    └─────────┬──────────┘
              ▼
  ┌───────────────────────────────────┐
  │  Draft Resume                     │
  │  Header → Education →             │
  │  Experience → Projects → Skills   │
  │  Bullet: Verb → Task → Result     │
  └───────────────────────────────────┘
              │
              ▼
  ┌──────────────────────┐
  │ Pass 1: ATS Gate     │ ← fail → revise
  └──────────────────────┘
              │
              ▼
  ┌──────────────────────┐
  │ Pass 2: Human Voice  │ ← fail → revise
  └──────────────────────┘
              │
              ▼
  ┌──────────────────────┐
  │ Pass 3: Hiring Mgr   │ ← fail → revise
  └──────────────────────┘
              │ all pass
              ▼
  ┌───────────────────────────────────┐
  │  Output: plain text or .docx      │
  └───────────────────────────────────┘
```

---

## 🧰 Skill Structure

```
claude-quant-resume-skill/
├── README.md
├── LICENSE                                      ← Apache 2.0
├── CONTRIBUTING.md
├── PR_BODY.md                                   ← PR template for anthropics/skills
└── skills/
    └── quant-resume-writer/
        ├── SKILL.md                             ← 6-step workflow + 4 modes + 3-pass review
        └── references/
            ├── ats-keywords.md                  ← Master keyword list by role & company
            ├── banned-phrases.md                ← Cliché blacklist with rewrite patterns
            ├── company-jd-signals.md            ← Per-company ATS platform & interview signals
            └── profile-extraction.md            ← GitHub API + LinkedIn extraction logic ← NEW
```

| File | Purpose |
|------|---------|
| `SKILL.md` | 6-step workflow, 4 modes, GitHub/LinkedIn intake, 3-pass review |
| `ats-keywords.md` | Master keyword list by sub-role and company |
| `banned-phrases.md` | Cliché blacklist with rewrite patterns |
| `company-jd-signals.md` | ATS platform per company + quirks + post-ATS signals |
| `profile-extraction.md` | GitHub API fetch, repo relevance scoring, LinkedIn methods, merge rules |

---

## 🚫 Anti-Fabrication Rules

| What | Rule |
|------|------|
| Job titles | Only exact title from LinkedIn/user. Never upgrades "intern" to "analyst" |
| Years of experience | Calculated from dates provided. Never rounded up |
| Skills | Only from GitHub imports + LinkedIn skills + user-confirmed |
| GPA | Only if provided AND ≥ 3.5 |
| Metrics | Only from README, LinkedIn, or user-confirmed. Never invented |
| Repo tech stack | Only from dependency files + topics. Never assumed |
| Repo stars | Social proof only — never used as a resume metric |

---

## 🛑 What Makes This Different

| Feature | This skill | Generic tools | Other open-source |
|---------|-----------|--------------|------------------|
| Pulls real projects from GitHub API | ✅ | ❌ | ❌ |
| Scores repos against JD keywords | ✅ | ❌ | ❌ |
| Extracts LinkedIn experience | ✅ | ❌ | ❌ |
| Merges GitHub + LinkedIn into richer bullets | ✅ | ❌ | ❌ |
| JD-Mirror mode (quant-specific) | ✅ | ❌ | ❌ |
| 3-pass review before output | ✅ | ❌ | ❌ |
| Per-company ATS platform map | ✅ | ❌ | ❌ |
| Hard anti-fabrication enforcement | ✅ | ❌ | ❌ |
| DOCX output (ATS-safe) | ✅ | ✅ | ❌ |
| Works in Claude.ai Skills | ✅ | N/A | N/A |

---

## 💡 Usage Examples

```bash
# Full extraction — GitHub + LinkedIn + JD (best result)
"Write me an ATS resume for Citadel QR.
 GitHub: github.com/myusername
 LinkedIn: [paste Experience + Education]
 JD: [paste Citadel job posting]"

# GitHub only, no LinkedIn
"Write me a quant resume targeting Jane Street.
 GitHub: github.com/myusername
 Here's my experience manually: [notes]"

# LinkedIn PDF upload
"Here's my LinkedIn export PDF [upload].
 Target: Quant Engineer at Two Sigma."

# JD-Mirror with GitHub only
"Here's the IMC Trading posting: [paste JD]
 Pull my projects from: github.com/myusername"

# Score existing resume
"Score my resume: [paste resume]"

# Get a Word file
"Write my resume and give me a .docx file."
```

---

## ⚙️ Customization

| What to change | Where |
|---------------|-------|
| Repo scoring weights | `references/profile-extraction.md` → JD-Relevance Scoring |
| Number of repos to scan | `references/profile-extraction.md` → `per_page=30` cutoff |
| Add a company | `references/company-jd-signals.md` |
| Add keywords | `references/ats-keywords.md` |
| Change review loop rules | `SKILL.md` → Step 5d |
| Change DOCX formatting | `SKILL.md` → Step 6 |

---

## 🤝 Contributing

PRs welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

Key areas:
- **Company signals** — hedge funds, quant boutiques, prop shops not yet covered
- **International ATS** — EU/UK, Singapore, HK, Canada
- **New roles** — risk quant, desk quant, quant structurer, actuarial
- **GitHub extraction** — better relevance heuristics, monorepo handling
- **LinkedIn** — improved PDF parsing, new section types
- **Test cases** — sample profiles + JDs + expected outputs

---

## 🗺️ Roadmap

### Done ✅
- [x] GitHub API extraction — repo scoring, tech stack, metrics from README
- [x] LinkedIn extraction — paste / PDF / public URL with graceful fallback
- [x] GitHub + LinkedIn merge into richer bullets
- [x] 4 modes: WRITE / OPTIMIZE / JD-MIRROR / SCORE
- [x] 3-pass internal review loop
- [x] JD keyword match report (Required / Partial / Absent)
- [x] Company-specific ATS platform map (12 companies)
- [x] DOCX output, ATS parse simulation, cover letter stub

### Planned 🔜
- [ ] Private repo support (optional user-provided GitHub token)
- [ ] International ATS patterns (EU/UK, Singapore, HK, Canada)
- [ ] LinkedIn PDF parser improvements
- [ ] Test case benchmark set
- [ ] LinkedIn headline / summary generator (JD-aware)
- [ ] Interview prep notes based on company signals

---

## 📖 Also Contributed To

This skill is submitted as a PR to [anthropics/skills](https://github.com/anthropics/skills).
Once merged, it's natively discoverable inside Claude.ai's Skills search.

---

## 🙏 Acknowledgements

- [anthropics/skills](https://github.com/anthropics/skills) — official skill examples and agentskills.io standard
- GitHub REST API — public repo access that makes zero-auth extraction possible

---


Apache 2.0 — see [LICENSE](LICENSE) · Made by [pooja2420](https://github.com/pooja2420)
