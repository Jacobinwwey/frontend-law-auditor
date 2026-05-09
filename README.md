# Frontend Law Auditor

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](./LICENSE.txt)
[![Python](https://img.shields.io/badge/python-3.x-blue.svg)](https://www.python.org/)
[![Laws](https://img.shields.io/badge/laws-21-orange.svg)](./rules/_sections.md)
[![Fast Gate Checks](https://img.shields.io/badge/fast_gate_checks-10-purple.svg)](./scripts/law_audit.py)

[English](./README.md) | [Chinese](./README.zh-CN.md)


Summerized Learning Basic Principle :
<img width="1914" height="13636" alt="image" src="https://github.com/user-attachments/assets/0bd258b7-6da1-4381-9efd-6bddc1b997f7" />


---

`frontend-law-auditor` is a standalone skill repository for auditing frontend UX quality with measurable, theory-grounded checks. It turns human-centered design laws into an executable gate so teams can detect friction early, prioritize fixes, and enforce a release threshold in CI.

## Features

- **Fast gate (10 checks)** for binary release readiness (touch target size, feedback latency, choice density, progress visibility, validation quality, and more).
- **Deep law diagnosis (21 principles)** covering Fitts, Hick, Gestalt family, Von Restorff, Jakob, Miller, Goal-Gradient, Zeigarnik, Tesler, Peak-End, Postel, Doherty, Serial Position, Occam, and Parkinson.
- **Weighted scoring model** with `pass/fail/unknown` outcomes and a normalized 0-100 score.
- **Actionable remediation output** with priority buckets and rule-file mapping for each failed principle.
- **CI-friendly strict mode** that returns non-zero when gate failures exist or score is below threshold.

## Prerequisites

- Python 3.x
- A measurable flow with evidence data (for example: signup, checkout, onboarding)

Check Python:

```bash
python --version
```

## Installation

```bash
git clone https://github.com/Jacobinwwey/frontend-law-auditor.git
cd frontend-law-auditor
```

No extra dependency install is required. The audit script uses Python standard library only.

## Quick Start

1. Create an evidence template.
2. Fill measured values from your real UI flow.
3. Run audit and inspect report.
4. Optional: enforce strict gate in CI.

```bash
# 1) Create template
python scripts/law_audit.py --init-template ./examples/evidence.local.json

# 2) Fill ./examples/evidence.local.json with measured values

# 3) Run audit report
python scripts/law_audit.py \
  --input ./examples/evidence.local.json \
  --output ./examples/audit.local.md \
  --json-out ./examples/audit.local.json

# 4) Strict gate (fails with non-zero exit code when below threshold)
python scripts/law_audit.py \
  --input ./examples/evidence.local.json \
  --strict \
  --fail-threshold 85
```

## Output Contract

Every audit run is expected to provide:

1. **Fast Gate Failures** with direct evidence.
2. **Law Diagnosis** in the shape of:
   `Principle -> Observed friction -> Why it happens -> UI change`.
3. **Priority Fix Plan** grouped by `P0/P1/P2`.
4. **Recheck Checklist** for the next audit round.

## Evidence Model

Input schema and thresholds are documented in:
- [references/metrics-schema.md](./references/metrics-schema.md)

Theory and implementation playbooks are documented in:
- [references/theory-playbook.md](./references/theory-playbook.md)
- [rules/_sections.md](./rules/_sections.md)
- `rules/<law>.md`

If key evidence is missing, affected laws are marked as `unknown`.

## Scoring and Strict Mode

- Principle score status:
  - `pass = 1.0`
  - `fail = 0.0`
  - `unknown = 0.4`
- Weighted total score:
  - normalized to `0-100`
- Strict mode fails when:
  - any fast gate check fails, or
  - score is lower than `--fail-threshold` (default `85`)

## Principles Covered

- Fitts's Law
- Hick's Law
- Gestalt: Proximity, Similarity, Continuity, Closure, Figure/Ground, Common Fate, Focal Point
- Von Restorff Effect
- Jakob's Law
- Miller's Law
- Goal-Gradient Hypothesis
- Zeigarnik Effect
- Tesler's Law
- Peak-End Rule
- Postel's Law
- Doherty Threshold
- Serial Position Effect
- Occam's Razor
- Parkinson's Law

## Repository Layout

```text
frontend-law-auditor/
|-- SKILL.md
|-- scripts/law_audit.py
|-- examples/evidence.sample.json
|-- references/
|   |-- metrics-schema.md
|   `-- theory-playbook.md
`-- rules/
    |-- _sections.md
    `-- *.md
```

## Contributing

- Keep `scripts/law_audit.py`, `references/metrics-schema.md`, and `rules/` consistent when adding or changing metrics/laws.
- Prefer measurable acceptance thresholds over subjective wording.
- Add or update sample evidence when changing scoring semantics.

## License

MIT License. See [LICENSE.txt](./LICENSE.txt).



![Star History Chart](https://api.star-history.com/svg?repos=Jacobinwwey/frontend-law-auditor&type=Date)
#### Friendly Links: [Linux DO：学AI，上L站！](https://linux.do/)
