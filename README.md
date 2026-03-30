# claude-quant-resume-skill ⚔️📄

> 🎯 **Let Claude write your quant resume while you sleep.** Wake up to a fully ATS-optimized, human-sounding resume — keywords extracted from the JD, clichés stripped, metrics surfaced, and a 3-pass internal review already done.
>
> 🪶 **Zero dependencies, zero lock-in.** The entire system is plain Markdown files. One `SKILL.md` readable by any Claude-compatible agent. Fork it, adapt it, make it yours.
>
> *💡 This is a methodology, not a platform. The resume workflow is what matters — take it anywhere. 🌱*

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Compatible with: Claude.ai](https://img.shields.io/badge/Claude.ai-Skills-blueviolet)](https://claude.ai)
[![ATS Target Score: 95+](https://img.shields.io/badge/ATS%20Score-95%2B-brightgreen)]()
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-orange.svg)](CONTRIBUTING.md)
[![agentskills.io](https://img.shields.io/badge/agentskills.io-standard-blue)](https://agentskills.io)

[💬 Contribute](#-contributing) · [📖 Skill Structure](#-skill-structure) · [🚀 Quick Start](#-quick-start) · [🏦 Target Companies](#-target-companies)

> ⭐ If this helped you land an interview, star the repo — it helps others find it.

---

## 🎯 More Than Just a Resume Builder

**Basic mode** — give Claude your background, it handles everything:
```
"Write me an ATS resume for a quant researcher role at Citadel. Here's my background: ..."
```

**🔥 JD-Mirror mode** — got a job posting? Give Claude the JD + your profile:
```
"Here's the Jane Street QR job posting: [paste JD]. Tailor my resume to it: [paste profile]"
```
Claude reads the JD → extracts required and preferred keywords → builds a match report → rewires every bullet to use the JD's exact phrasing. No other open-source resume skill does this for quant roles.

**🔥 Score mode** — already have a resume?
```
"Score my resume against quant ATS standards: [paste resume]"
```
Returns a per-category audit with a score out of 100 and top-3 specific fixes to reach 95+.

---

## 📈 What the 3-Pass Review Loop Does

Every resume goes through three internal passes **before any output is produced** — so it reads like a human wrote it, not an AI.

| Pass | What it checks | What it fixes |
|------|---------------|---------------|
| **① ATS Gate** | Keywords, date format, section headers, banned phrases, fabrication check | Hard formatting and keyword failures |
| **② Human Voice Check** | Passive voice, identical bullet rhythm, AI filler words, vague bullets | Rewrites bullets to sound specific and owned |
| **③ Hiring Manager Scan** | Strongest line on page 1, logical narrative, skills match bullets | Restructures narrative arc, removes noise |

If any pass fails → revise → re-run all 3 passes. Only then does output happen.

**Real example — before / after Pass 2:**

| ❌ Before | ✅ After |
|-----------|---------|
| "Responsible for data analysis in a fast-paced environment" | "Analyzed 3 years of order-book tick data in Python, identifying a mean-reversion signal with 0.42 Sharpe across 12 equity pairs" |
| "Helped develop machine learning models for trading" | "Built an XGBoost price-direction classifier on 18 months of 1-min OHLCV data, achieving 54.2% directional accuracy vs 50.8% baseline" |
| "Good communication skills, team player" | *(deleted — replaced with a concrete bullet)* |

---

## 🚀 Quick Start

### Option 1: Claude.ai Skills UI
```
1. Download quant-resume-writer.skill from Releases
2. Claude.ai → Settings → Skills → Upload Skill
3. Start a new chat — skill activates automatically
```

### Option 2: Claude Code / API
```bash
git clone https://github.com/pooja2420/claude-quant-resume-skill.git
cp -r claude-quant-resume-skill/skills/quant-resume-writer ~/.claude/skills/
claude
```

### Option 3: Manual (any Claude interface)
Upload `skills/quant-resume-writer/SKILL.md` directly as a skill file or system prompt addition.

---

## 🧩 Four Modes

| Mode | Trigger | Use when | ATS lift |
|------|---------|----------|---------|
| `WRITE` | "write my resume" | Starting from scratch | Baseline |
| `OPTIMIZE` | "improve my resume" + paste | Existing resume needs work | +15–25 pts |
| `JD-MIRROR` | Paste a job description | Tailoring to one specific role | +25–40 pts |
| `SCORE` | "score my resume" | Auditing without rewriting | — (report only) |

> 💡 **Auto-detection:** If you paste a job description, JD-Mirror activates automatically. No need to specify the mode.

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
| Amazon | Workday | Hard keyword match — exact phrase matters. LP assessed in interview |
| Google | gHire | GPA and school weighted. Algorithmic problem-solving emphasized |
| Meta | Greenhouse | PyTorch, open-source ML. GitHub links scanned |
| Microsoft | Workday | Breadth valued. Azure, ML, system design |
| Apple | Workday | On-device ML, efficiency, privacy-preserving ML |
| Netflix | Lever | Experimentation at scale, A/B testing, personalization |
| Walmart / CVS | Workday / Taleo | Supply chain / health analytics. Taleo strips all formatting aggressively |

> ⚠️ **Workday tip**: Use `Month YYYY – Month YYYY` date format only. Workday rejects slashes and ordinals.
>
> ⚠️ **Taleo tip** (CVS): Use the plainest possible formatting. No special characters in section headers.

---

## 🔄 Full Workflow

```
User provides profile + (optional) JD
         │
         ▼
┌─────────────────────┐
│   Mode Detection    │  ← auto-detects WRITE / OPTIMIZE / JD-MIRROR / SCORE
└─────────────────────┘
         │
    ┌────┴──────────────────────┐
    │                           │
    ▼                           ▼
[JD-MIRROR]               [WRITE / OPTIMIZE]
Extract keywords          Use profile as-is
Build match report
    │                           │
    └──────────┬────────────────┘
               ▼
    ┌─────────────────────┐
    │   Draft Resume      │  ← Structure: Header → Education → Experience → Projects → Skills
    │   (Steps 1–4)       │  ← Bullet formula: Action Verb → Task → Quantified Result
    └─────────────────────┘
               │
               ▼
    ┌─────────────────────┐
    │  Pass 1: ATS Gate   │  ← Keywords ✓  Dates ✓  Headers ✓  No fabrication ✓
    └─────────────────────┘
               │ fail → revise
               ▼
    ┌─────────────────────┐
    │  Pass 2: Human      │  ← No passive voice ✓  Varied rhythm ✓  Specific nouns ✓
    │  Voice Check        │
    └─────────────────────┘
               │ fail → revise
               ▼
    ┌─────────────────────┐
    │  Pass 3: Hiring     │  ← Best line on page 1 ✓  Narrative arc ✓  Skills = bullets ✓
    │  Manager Scan       │
    └─────────────────────┘
               │ all pass
               ▼
    ┌─────────────────────┐
    │      Output         │  ← Plain text (default) or .docx (on request)
    └─────────────────────┘
```

---

## 🧰 Skill Structure

```
claude-quant-resume-skill/
├── README.md
├── LICENSE                                   ← Apache 2.0
├── CONTRIBUTING.md
├── PR_BODY.md                                ← PR template for anthropics/skills
└── skills/
    └── quant-resume-writer/
        ├── SKILL.md                          ← 6-step workflow + 4 modes + 3-pass review
        └── references/
            ├── ats-keywords.md               ← Master keyword list by role & company
            ├── banned-phrases.md             ← Cliché blacklist with rewrite patterns
            └── company-jd-signals.md         ← Per-company ATS platform & interview signals
```

**`SKILL.md`** — the brain. Six steps:
1. Profile intake (one structured ask, nothing assumed)
2. ATS pre-flight check
3. Resume structure (strict section order every ATS can parse)
4. Bullet writing rules (Action Verb → Task → Quantified Result)
5. JD-Mirror + ATS keyword injection + parse simulation + **3-Pass Review Loop**
6. Output (plain text or .docx with ATS-safe formatting)

**`references/ats-keywords.md`** — master keyword list organized by sub-role: Quant Researcher, Quant Engineer, Entry-Level, Big Tech Quant, CVS/Walmart.

**`references/banned-phrases.md`** — full cliché blacklist with rewrite patterns. Not just deletion — every banned phrase includes a replacement instruction.

**`references/company-jd-signals.md`** — maps each of the 12 target companies to its ATS platform, platform-specific quirks, and what comes after the ATS screen.

---

## 🚫 Anti-Fabrication Rules (non-negotiable)

| What | Rule |
|------|------|
| Job titles | Only the exact title you held. Never upgrades "intern" to "analyst" |
| Years of experience | Calculated from dates you provide. Never rounded up |
| Skills | Only what you've mentioned or confirmed. Never adds "common" skills |
| GPA | Only included if you provide it AND it is ≥ 3.5 |
| Metrics | Only numbers you provide. Asks if uncertain |
| Publications / awards | Only what you explicitly state |

If you ask Claude to "add more" without providing real data:
> *"I can't add skills or experience you haven't mentioned — that would be fabrication and could get you screened out or fired. Can you tell me more about what you actually worked on?"*

---

## 🛑 What Makes This Different

| Feature | This skill | Generic resume tools | Other open-source |
|---------|-----------|---------------------|------------------|
| JD-Mirror mode (quant-specific) | ✅ | ❌ | ❌ |
| 3-pass internal review before output | ✅ | ❌ | ❌ |
| Per-company ATS platform map (12 firms) | ✅ | ❌ | ❌ |
| Hard anti-fabrication enforcement | ✅ | ❌ | ❌ |
| ATS parse simulation (invisible failures) | ✅ | Partial | ❌ |
| Banned-phrase blacklist with rewrites | ✅ | Partial | Partial |
| DOCX output (ATS-safe format) | ✅ | ✅ | ❌ |
| SCORE mode (per-category audit) | ✅ | Partial | ❌ |
| Cover letter stub (JD-aware) | ✅ | Partial | ❌ |
| Works in Claude.ai Skills | ✅ | N/A | N/A |

---

## 💡 Usage Examples

```
# Write from scratch
"Write me an ATS resume for a quant researcher role at Citadel. Here's my background:
 - MS Statistics, University of Chicago, 2024, GPA 3.9
 - Quant Research Intern, Two Sigma, Summer 2023
 - Projects: pairs trading strategy in Python, Monte Carlo option pricer in C++
 - Skills: Python, C++, R, NumPy, pandas, stochastic calculus, probability"

# JD-Mirror mode — paste the actual job description
"Here's the Jane Street QR job posting: [paste full JD text]
 Here's my profile: [paste background]
 Please tailor my resume to this role."

# Score and audit only
"Score my resume against quant ATS standards: [paste resume]"

# Get a Word file
"Write my resume and give me a .docx file."

# Cover letter (offered automatically after resume is done)
"Now write a 3-paragraph cover letter for Jane Street."
```

---

## ⚙️ Customization

The skill is plain Markdown. Fork and adapt:

| What to change | Where | How |
|---------------|-------|-----|
| Add a company | `references/company-jd-signals.md` | Follow existing format — ATS platform, quirks, signals |
| Add keywords | `references/ats-keywords.md` | Add under the relevant role section |
| Add banned phrases | `references/banned-phrases.md` | Add phrase + rewrite pattern |
| Change review loop | `SKILL.md` → Step 5d | Edit Pass 1/2/3 checklists |
| Change DOCX formatting | `SKILL.md` → Step 6 | Edit font, margins, section header style |

---

## 🤝 Contributing

PRs welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

Key areas:
- **Company signals** — JD patterns for firms not yet covered (hedge funds, quant boutiques, prop shops)
- **International ATS** — EU/UK (Europass), Singapore, Hong Kong, Canada
- **New role coverage** — risk quant, desk quant, quant structurer, actuarial, systematic macro
- **Keyword updates** — new tools entering quant stacks (Rust, JAX, Triton)
- **Test cases** — sample profiles + JDs + expected outputs to benchmark quality

Ground rules:
1. No fabrication — never add keywords not verified from real JDs
2. Cite your source — note where company signals come from (anonymized is fine)
3. Keep it concise — the skill is read token by token; every line costs
4. Test before PR — run a sample resume through Claude with your change

---

## 🗺️ Roadmap

### Done ✅
- [x] 4 modes: WRITE / OPTIMIZE / JD-MIRROR / SCORE
- [x] 3-pass internal review loop (ATS Gate → Human Voice → Hiring Manager)
- [x] JD keyword match report with Required / Partial / Absent classification
- [x] Company-specific ATS platform map (12 companies, 6 ATS platforms)
- [x] Per-company interview signal notes
- [x] DOCX output (ATS-safe, no tables, correct bullet format)
- [x] ATS parse simulation (catches invisible failures before output)
- [x] Banned-phrase blacklist with rewrite patterns
- [x] Cover letter stub (JD-aware, offered after resume)
- [x] Anti-fabrication hard rules with explanations

### Planned 🔜
- [ ] International ATS patterns (EU/UK, Singapore, HK, Canada)
- [ ] Additional role coverage (risk quant, desk quant, quant structurer)
- [ ] Test case benchmark set — sample profiles + JDs + scored outputs
- [ ] LinkedIn summary generator (mirrors resume, JD-aware)
- [ ] Interview prep stub — role-specific prep notes based on company signals

---

## 📖 Also Contributed To

This skill is submitted as a PR to [anthropics/skills](https://github.com/anthropics/skills) — Anthropic's official open-source skills repository. Once merged, it becomes natively discoverable inside Claude.ai's Skills search.

---

## 🙏 Acknowledgements

Inspired by:
- [ARIS](https://github.com/wanshuiyin/Auto-claude-code-research-in-sleep) — autonomous research workflows with Claude Code; the model for how a Claude skill repo should be structured
- [anthropics/skills](https://github.com/anthropics/skills) — Anthropic's official skill examples and agentskills.io standard

---

## ⭐ Star History

[![Star History Chart](https://api.star-history.com/svg?repos=pooja2420/claude-quant-resume-skill&type=Date)](https://star-history.com/#pooja2420/claude-quant-resume-skill&Date)

---

## License

Apache 2.0 — see [LICENSE](LICENSE).  
Made by [pooja2420](https://github.com/pooja2420)
