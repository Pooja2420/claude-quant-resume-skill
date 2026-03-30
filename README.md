# claude-quant-resume-skill

> A Claude skill that writes ATS-optimized resumes for quant finance and tech roles — with zero fabrication.

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Compatible with: Claude.ai](https://img.shields.io/badge/Claude.ai-Skills-blueviolet)](https://claude.ai)
[![ATS Target Score: 95+](https://img.shields.io/badge/ATS%20Score-95%2B-brightgreen)]()

## What it does

Produces ATS-ready resumes for entry-level and experienced quant roles at:

**Quant Firms:** Citadel · Jane Street · IMC Trading · Two Sigma · DE Shaw · Nasdaq  
**Big Tech:** Amazon · Google · Meta · Microsoft · Apple · Netflix · Walmart · CVS

### Four modes

| Mode | Trigger | Use when |
|------|---------|----------|
| `WRITE` | "write my resume" | Starting from scratch |
| `OPTIMIZE` | "improve my resume" + paste | Existing resume needs work |
| `JD-MIRROR` | Paste a job description | Maximizing ATS keyword match for one role |
| `SCORE` | "score my resume" | Auditing without rewriting |

### What makes this different

- **JD-Mirror mode** — ingests the actual job posting, extracts required vs. preferred keywords, outputs a match report, then rewrites bullets to use the JD's exact phrasing. No other open-source resume tool does this for quant roles.
- **Company-specific ATS signals** — maps each firm to its ATS platform (Workday, Greenhouse, Lever, Taleo) and surfaces platform-specific quirks that silently kill good resumes.
- **Hard anti-fabrication** — refuses to invent skills, titles, years of experience, or metrics. Explains why when asked.
- **ATS parse simulation** — catches invisible failures: wrong date format, non-standard section headers, name in a text box.
- **Banned-phrase blacklist** — not just deletion, includes rewrite patterns for every cliché.
- **SCORE mode** — per-category audit with specific top-3 fixes to reach 95+.
- **DOCX output** — ATS-safe Word file on request (no tables, no columns, correct bullet format).

---

## Installation

### In Claude.ai (Skills)

1. Download [`claude-quant-resume-skill.skill`](releases/latest)
2. Go to **Claude.ai → Settings → Skills → Upload Skill**
3. Upload the `.skill` file
4. Start a new chat and ask Claude to write or optimize your resume

### Manual (Claude Code / API)

```bash
git clone https://github.com/pooja2420/claude-quant-resume-skill.git
```

Point Claude at the `skills/claude-quant-resume-skill/` folder or upload `SKILL.md` directly.

---

## Usage examples

```
"Write me an ATS resume for a quant researcher role at Citadel. Here's my background: ..."

"Here's the Jane Street QR job posting [paste JD]. Tailor my resume to it: ..."

"Score my resume against quant ATS standards: [paste resume]"

"Optimize my resume and give me a .docx file"
```

---

## Skill structure

```
skills/claude-quant-resume-skill/
├── SKILL.md                          # Main instructions (6-step workflow)
└── references/
    ├── ats-keywords.md               # Master keyword list by role & company
    ├── banned-phrases.md             # Cliché blacklist with rewrite patterns
    └── company-jd-signals.md        # Per-company ATS platform & interview signals
```

---

## Contributing

PRs welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

Key areas for contribution:
- Additional company JD signals (hedge funds, quant boutiques)
- International ATS patterns (EU, UK, Singapore, HK)
- Additional role coverage (risk quant, desk quant, quant structurer)
- Test cases and ATS score benchmarks

---

## Also contributed to

This skill is also submitted as a PR to [anthropics/skills](https://github.com/anthropics/skills) — Anthropic's official open-source skills repository.

---

## License

Apache 2.0 — see [LICENSE](LICENSE).
