# Copyright 2026 pooja2420 — Apache License 2.0
# https://www.apache.org/licenses/LICENSE-2.0

---
name: quant-resume-writer
description: >
  Use this skill to write, rewrite, or optimize a resume for entry-level or experienced
  quant roles — including Quantitative Researcher, Quantitative Analyst, Quantitative
  Engineer, Quant Developer, Algorithmic Trader, or Risk Analyst — at elite firms such as
  Citadel, Jane Street, IMC Trading, Two Sigma, DE Shaw, Nasdaq, or large tech companies
  (Amazon, Google, Meta, Apple, Microsoft, Netflix, Walmart). Trigger this skill whenever
  the user says: "write my resume", "update my resume", "tailor my resume for quant",
  "ATS resume", "make my resume for [company]", or uploads/pastes their current resume and
  asks to improve it for quant or tech roles. Also trigger when the user says "optimize for
  ATS", "quant job resume", "entry level quant", or "help me apply to [quant firm]".
  Output is plain text by default; produce a .docx if the user requests it.
  NEVER fabricate skills, titles, years of experience, or metrics the user has not provided.
---

# Quant Resume Writer

Produces ATS-optimized, honest, concise resumes targeting entry-level and experienced
quant roles at Tier-1 firms. Targets 95+ ATS score by the standards of
Amazon, Citadel, Jane Street, Meta, Microsoft, Google, Netflix, IMC Trading,
Nasdaq, Apple, Walmart, and CVS.

**Modes:**
- `WRITE` — build resume from scratch (default)
- `OPTIMIZE` — improve an existing resume the user pastes
- `JD-MIRROR` — tailor resume to a specific job description (highest ATS lift)
- `SCORE` — audit an existing resume and return a scored report only

If the user pastes/uploads a JD or job URL, automatically activate **JD-MIRROR** mode.

---

## Step 0 — Gather Profile

If the user has NOT provided their background, ask for ALL of the following in one message:

1. Full name, location (city/state), LinkedIn URL, GitHub URL, email
2. Education: school, degree, major, GPA (if ≥ 3.5), graduation year
3. Work/internship experience: title, company, dates, responsibilities (paste raw bullets OK)
4. Projects: name, tech stack, outcomes/metrics if any
5. Skills: programming languages, tools, frameworks, math areas
6. Target role and target companies (or confirm defaults above)
7. Any publications, competitions, or awards

**Never invent or embellish any of the above.** If info is absent, leave that section out or
flag it to the user.

---

## Step 1 — ATS Pre-Flight Check

Before writing, mentally audit the profile against these ATS requirements:

| Check | Rule |
|-------|------|
| Keywords | Role-critical terms must appear verbatim (see references/ats-keywords.md) |
| Titles | Use standard industry titles only; do not fabricate promotions |
| Dates | Use `Month YYYY – Month YYYY` or `Month YYYY – Present` format |
| Metrics | Include quantified impact wherever the user has provided numbers |
| Sections | Header, Education, Experience, Projects, Skills — in this order |
| File format | Plain text output unless docx requested |
| Length | 1 page for ≤2 years XP; up to 2 pages for senior; ruthlessly trim filler |
| Clichés | Strip all negative clichés (see references/banned-phrases.md) |

---

## Step 2 — Resume Structure

Follow this exact section order. Use **clean, ATS-parseable headings** (no icons, no tables,
no text boxes, no columns).

```
[FULL NAME]
[City, State] | [email] | [LinkedIn] | [GitHub]

EDUCATION
[Degree], [Major] — [University]                     [Month YYYY]
GPA: X.XX/4.00 (include only if ≥ 3.5)
Relevant Coursework: [list 4–6 quant-relevant courses]

EXPERIENCE
[Job Title] — [Company], [City]                  [Month YYYY – Month YYYY]
• [Action verb] + [what you did] + [result/metric]
• (3–5 bullets per role; each ≤ 2 lines)

PROJECTS
[Project Name] | [Tech Stack]                       [Month YYYY]
• [What it does + outcome/metric]

SKILLS
Languages: Python, C++, R, SQL, MATLAB, Julia
Math: Stochastic Calculus, Linear Algebra, Probability, Statistics, ML
Tools: NumPy, Pandas, scikit-learn, PyTorch, Git, Bloomberg
```

---

## Step 3 — Bullet Writing Rules

Each bullet must follow: **Action Verb → Task → Quantified Result**

✅ Good:
- "Implemented a pairs-trading strategy in Python, achieving 18% annualized return in backtests on 5 years of tick data"
- "Reduced Monte Carlo simulation runtime by 40% via vectorized NumPy operations"
- "Built a real-time order-book feature pipeline processing 200k events/sec"

❌ Bad (strip these):
- "Responsible for..." → rewrite as active
- "Helped with..." → rewrite as owned
- "Worked on a team..." → rewrite with your specific contribution
- "Good communication skills" → delete
- "Hard-working, detail-oriented" → delete
- "Fast learner" → delete

If the user has NOT provided a metric, use one of these honest hedges:
- "contributing to a X% improvement in [area]" — **only if the user confirms the number**
- Leave the metric blank rather than fabricate one
- Ask the user: "Do you have any metrics for this role (e.g., size of dataset, runtime improvements, P&L impact)?"

---

## Step 4 — ATS Keyword Injection

Read `references/ats-keywords.md` for the master keyword list organized by role.

Inject keywords **naturally** into bullets, skills, and coursework — never keyword-stuff
or list keywords in a hidden section.

Priority keywords for quant roles (always include relevant ones):
- **Languages**: Python, C++, R, SQL
- **Math**: stochastic calculus, probability, statistics, linear algebra, optimization
- **Finance**: derivatives, options pricing, Monte Carlo, backtesting, risk management,
  alpha generation, market microstructure, factor models, fixed income
- **ML**: machine learning, regression, time series, neural networks, NLP, reinforcement learning
- **Systems**: low-latency, real-time, distributed systems, data pipelines

---

## Step 5 — ATS Scoring Self-Check

After drafting, score the resume against this rubric to ensure 95+:

| Category | Weight | Criteria |
|----------|--------|----------|
| Keyword density | 30% | ≥8 role-critical keywords present |
| Formatting | 20% | No tables/columns/graphics; standard section names |
| Metrics | 20% | ≥50% of bullets have quantified impact |
| Honest accuracy | 15% | Zero fabricated info |
| Conciseness | 10% | No filler phrases; bullets ≤2 lines each |
| Action verbs | 5% | All bullets start with strong past-tense verbs |

If any category falls short, revise before outputting.

---

## Step 5b — JD-Mirror Mode (activate when JD is provided)

This is the single highest-impact ATS lever. No other open-source tool does this for quant roles.

**Process:**
1. Extract from the JD: required skills, preferred skills, exact role title, years of XP asked, tools mentioned, verbs used in responsibilities section
2. Build a **JD Keyword Hit List** — two columns: `Required` / `Preferred`
3. For each keyword the user's profile legitimately covers, inject it **verbatim** (same spelling, same capitalization) into a bullet or skills line
4. For keywords the user does NOT have: flag them honestly — do NOT fabricate

**Output the Hit List before the resume:**
```
JD KEYWORD MATCH REPORT
========================
✅ Matched (inject):    Python, C++, Monte Carlo, options pricing, backtesting
⚠️  Partial (reframe):  "machine learning" → user has scikit-learn projects
❌ Absent (flag):       FPGA, Rust — user lacks these, do not add
JD Match Score: 87% (11/13 required keywords covered)
```

**Company-specific JD signals** (from `references/company-jd-signals.md`):
- If JD is from **Citadel / Jane Street / IMC**: flag if problem-solving/math test likely → add note
- If JD is from **Amazon**: note Leadership Principles likely assessed in interview
- If JD is from **Google**: flag coding interview focus, suggest LeetCode prep note

---

## Step 5c — ATS Parse Simulation

Before outputting, mentally simulate how a dumb ATS parser reads the resume:

1. **Name extraction**: Is the name on its own line at the very top? (Not in a header/text box)
2. **Contact parsing**: Are email, phone, LinkedIn on the same or next line, pipe-separated?
3. **Date parsing**: Are all dates `Mon YYYY` or `YYYY` — no slashes, no ordinals?
4. **Section detection**: Do section names exactly match standard labels?
   - ✅ `EDUCATION`, `EXPERIENCE`, `SKILLS`, `PROJECTS`
   - ❌ `MY JOURNEY`, `TECH STACK`, `WHAT I'VE BUILT`
5. **Bullet parsing**: No sub-bullets (ATS often drops them); all bullets flush left
6. **File safety**: Warn user if docx — do not save as `.doc`, never submit `.pages`

If any parse issue found, fix it before Step 6.

---

## Step 6 — Output

**Plain text (default):**  
Output the resume in clean markdown-style plain text, suitable for copy-paste into any ATS.

**DOCX (if user requests "docx", "Word file", "download", or "save as file"):**  
Read `/mnt/skills/public/docx/SKILL.md`, then generate a `.docx` using `docx` npm package.

DOCX formatting rules for resumes:
- Font: Calibri 11pt body, 14pt name, 11pt section headers bold
- Margins: 0.75 inch all sides (to maximize content space)
- Section headers: All-caps, bold, with a thin bottom border line
- Bullets: Use `LevelFormat.BULLET` (never unicode •)
- No tables, no text boxes, no columns — ATS will fail on them
- US Letter page size (12240 × 15840 DXA)
- File saved to `/mnt/user-data/outputs/resume_[lastname].docx`

**SCORE mode output** (when user asks "score my resume" or "audit"):
```
ATS AUDIT REPORT
=================
Overall Score: XX/100
Keyword Density:   XX/30  — missing: [list]
Formatting:        XX/20  — issues: [list]
Metrics:           XX/20  — X of Y bullets lack quantification
Honest accuracy:   XX/15
Conciseness:       XX/10
Action verbs:      XX/5
Top 3 fixes to reach 95+:
  1. [specific fix]
  2. [specific fix]
  3. [specific fix]
```

**Cover letter stub** (offer after resume is done):
> "Want a 3-paragraph cover letter to accompany this for [Company]?
> I'll mirror JD language and avoid all clichés — same no-fabrication rules apply."

---

## Anti-Fabrication Rules (non-negotiable)

1. **Title**: Only use the exact title the user held. Do not upgrade "intern" to "analyst".
2. **Years of experience**: Calculate from dates the user provides. Do not round up.
3. **Skills**: Only list skills the user has mentioned or confirmed. Do not add "common" skills.
4. **GPA**: Only include if user provides it AND it is ≥ 3.5.
5. **Metrics**: Only include numbers the user provides. If uncertain, ask.
6. **Publications/Awards**: Only include what user explicitly states.

If the user asks you to "add more" without providing real data, respond:
> "I can't add skills or experience you haven't mentioned — that would be fabrication and
> could get you screened out or fired. Can you tell me more about what you actually worked on?"

---

## Negative Cliché Blacklist

See `references/banned-phrases.md` for the full list. Core banned phrases:
- "team player", "go-getter", "self-starter", "detail-oriented", "hardworking"
- "responsible for", "duties included", "helped with", "assisted in"
- "results-driven", "dynamic", "passionate about", "synergy", "leverage"
- "excellent communication skills", "strong work ethic", "fast learner"

Replace with concrete actions and results.

---

## Quick Reference: Strong Quant Action Verbs

**Built/Implemented**: Engineered, Developed, Implemented, Built, Deployed, Architected  
**Analyzed**: Analyzed, Modeled, Quantified, Estimated, Forecasted, Benchmarked  
**Improved**: Optimized, Reduced, Accelerated, Improved, Increased, Streamlined  
**Research**: Researched, Investigated, Derived, Proved, Validated, Backtested  
**Led**: Led, Designed, Owned, Directed, Coordinated (use sparingly; prefer individual ownership)
