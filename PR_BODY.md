## Summary

Adds a domain-specific resume skill for quant finance and tech roles — the first career-focused skill in this repo.

## What's included

**4 files** under `skills/claude-quant-resume-skill/`:

| File | Purpose |
|------|---------|
| `SKILL.md` | 6-step workflow, 4 modes (WRITE / OPTIMIZE / JD-MIRROR / SCORE) |
| `references/ats-keywords.md` | Master keyword list by sub-role and company |
| `references/banned-phrases.md` | Cliché blacklist with rewrite patterns |
| `references/company-jd-signals.md` | Per-company ATS platform map + interview signals |

## Target companies

Citadel · Jane Street · IMC Trading · Two Sigma · DE Shaw · Nasdaq  
Amazon · Google · Meta · Microsoft · Apple · Netflix · Walmart · CVS

## What makes this different from existing tools

- **JD-Mirror mode** — ingests a job posting, extracts required/preferred keywords, outputs a match report, rewires bullets to the JD's exact phrasing. No existing open-source resume tool does this for quant roles specifically.
- **Company ATS platform map** — each firm mapped to Workday / Greenhouse / Lever / Taleo with platform-specific quirks (e.g. Workday strict date format, Taleo strips formatting).
- **Hard anti-fabrication enforcement** — refuses to invent skills, titles, YOE, or metrics. Explains why if asked.
- **ATS parse simulation** — catches invisible failures before output.
- **SCORE mode** — per-category audit with top-3 specific fixes.
- **DOCX output** — ATS-safe Word file (no tables, no columns, correct LevelFormat.BULLET).

## Testing

Tested with Claude Sonnet 4.6 on:
- Entry-level profile → Citadel QR JD → JD-Mirror mode
- Existing resume paste → OPTIMIZE mode
- SCORE mode audit

## License

Apache 2.0 (matches repo license)

## Checklist

- [x] `SKILL.md` has valid YAML frontmatter (`name`, `description`)
- [x] No API keys or credentials in any file
- [x] References folder documented in SKILL.md
- [x] Apache 2.0 compatible
- [x] Follows progressive disclosure pattern (SKILL.md < 500 lines)
