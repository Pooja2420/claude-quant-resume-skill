# claude-quant-resume-skill

> A Claude skill that writes ATS-optimized resumes for quant finance and tech roles — with a built-in 3-pass review loop and zero fabrication.

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Compatible with: Claude.ai](https://img.shields.io/badge/Claude.ai-Skills-blueviolet)](https://claude.ai)
[![ATS Target Score: 95+](https://img.shields.io/badge/ATS%20Score-95%2B-brightgreen)]()
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-orange.svg)](CONTRIBUTING.md)

> ⭐ If this helped you land an interview, star the repo — it helps others find it.

---

## What it does

Produces ATS-ready resumes for entry-level and experienced quant roles at:

**Quant Firms:** Citadel · Jane Street · IMC Trading · Two Sigma · DE Shaw · Nasdaq  
**Big Tech:** Amazon · Google · Meta · Microsoft · Apple · Netflix · Walmart · CVS

---

## Four modes

| Mode | Trigger | Use when |
|------|---------|----------|
| `WRITE` | "write my resume" | Starting from scratch |
| `OPTIMIZE` | "improve my resume" + paste | Existing resume needs work |
| `JD-MIRROR` | Paste a job description | Maximizing ATS keyword match for one role |
| `SCORE` | "score my resume" | Auditing without rewriting |

---

## What makes this different

### 🔄 3-Pass Internal Review Loop
Most AI resume tools output on the first draft. This skill runs three internal checks **before producing any output** — so the resume reads like a human wrote it, not an AI.

| Pass | What it checks |
|------|---------------|
| **① ATS Gate** | Keywords, date format, section headers, zero banned phrases, ≥50% bullets quantified |
| **② Human Voice Check** | No passive voice, no identical bullet rhythm, no AI filler words, specific proper nouns anchoring each role |
| **③ Hiring Manager Scan** | Strongest line on page 1, logical narrative arc, skills section matches what bullets demonstrate |

If any pass fails → revise → re-run all 3 passes. Only then does output happen.

### 🎯 JD-Mirror Mode
Ingests the actual job posting, extracts required vs. preferred keywords, outputs a keyword match report, then rewrites bullets to use the JD's exact phrasing. No other open-source resume tool does this for quant roles specifically.

```
JD KEYWORD MATCH REPORT
========================
✅ Matched:   Python, C++, Monte Carlo, options pricing, backtesting
⚠️  Partial:  "machine learning" → user has scikit-learn projects  
❌ Absent:    FPGA, Rust — not added (anti-fabrication rule)
Match Score:  87% (11/13 required keywords covered)
```

### 🏦 Company-specific ATS signals
Maps each firm to its ATS platform and surfaces platform-specific quirks:

| Company | ATS Platform | Key quirk |
|---------|-------------|-----------|
| Amazon | Workday | Hard keyword match — exact phrase matters |
| Google | gHire | GPA and school weighted |
| Citadel | Lever | Human-first after basic filter |
| Jane Street | Internal | Very human-driven; résumé is a conversation starter |
| Meta | Greenhouse | GitHub links scanned |
| Apple | Workday | On-device ML and efficiency signals valued |

### 🚫 Zero fabrication
Hard rule — refuses to invent skills, titles, years of experience, or metrics. Every fact is traceable to what you provided. Explains why when asked.

### Other features
- **ATS parse simulation** — catches invisible failures: wrong date format, non-standard section headers, name in a text box
- **Banned-phrase blacklist** — not just deletion, includes rewrite patterns for every cliché
- **SCORE mode** — per-category audit with specific top-3 fixes to reach 95+
- **DOCX output** — ATS-safe Word file on request (no tables, no columns, correct bullet format)

---

## Installation

### Claude.ai (Skills)
1. Download [`quant-resume-writer.skill`](../../releases/latest)
2. Go to **Claude.ai → Settings → Skills → Upload Skill**
3. Upload the `.skill` file
4. Start a new chat — the skill activates automatically when you ask about your resume

### Claude Code / API
```bash
git clone https://github.com/pooja2420/claude-quant-resume-skill.git
```
Point Claude at the `skills/quant-resume-writer/` folder or upload `SKILL.md` directly via the Skills API.

---

## Usage examples

```
# Write from scratch
"Write me an ATS resume for a quant researcher role at Citadel. Here's my background: ..."

# JD-Mirror mode — highest ATS lift
"Here's the Jane Street QR job posting: [paste JD]. Tailor my resume to it: [paste profile]"

# Score existing resume
"Score my resume against quant ATS standards: [paste resume]"

# Get a Word file
"Optimize my resume and give me a .docx file"
```

---

## Repo structure

```
claude-quant-resume-skill/
├── README.md
├── LICENSE                           # Apache 2.0
├── CONTRIBUTING.md
├── PR_BODY.md                        # PR description for anthropics/skills
└── skills/
    └── quant-resume-writer/
        ├── SKILL.md                  # 6-step workflow + 4 modes
        └── references/
            ├── ats-keywords.md       # Master keyword list by role & company
            ├── banned-phrases.md     # Cliché blacklist with rewrite patterns
            └── company-jd-signals.md # Per-company ATS platform & interview signals
```

---

## Contributing

PRs welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

Key areas:
- Additional company JD signals (hedge funds, quant boutiques)
- International ATS patterns (EU, UK, Singapore, HK)
- Additional role coverage (risk quant, desk quant, quant structurer)
- Test cases and ATS score benchmarks

---

## Also contributed to

This skill is submitted as a PR to [anthropics/skills](https://github.com/anthropics/skills) — Anthropic's official open-source skills repository. Once merged, it becomes natively discoverable inside Claude.ai's Skills search.

---

## License

Apache 2.0 — see [LICENSE](LICENSE).
