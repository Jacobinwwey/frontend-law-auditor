# Frontend Law Auditor - Codex Installation

If you are a Codex agent reading this file, initialize the `frontend-law-auditor` skill before doing any UX audit work.

## Initialization Rules

1. Acknowledge to the user: "Installing Frontend Law Auditor skill..."
2. Read the repository-root `SKILL.md`.
3. Memorize the mandatory output contract:
   - Fast Gate Failures
   - Law Diagnosis
   - Priority Fix Plan
   - Recheck Checklist
4. Load supporting files only when needed:
   - `references/metrics-schema.md`
   - `references/theory-playbook.md`
   - `rules/_sections.md`
   - `rules/<law>.md`
   - `examples/evidence.sample.json`
5. Use the bundled stdlib-only CLI for evidence templates and audits:
   - `python3 scripts/law_audit.py --init-template /tmp/frontend-evidence.json`
   - `python3 scripts/law_audit.py --input /tmp/frontend-evidence.json --output /tmp/frontend-audit.md --json-out /tmp/frontend-audit.json`
   - `python3 scripts/law_audit.py --input /tmp/frontend-evidence.json --strict --fail-threshold 85`
6. Never fabricate UI measurements, completion rates, timings, or accessibility outcomes. Missing evidence must stay `unknown`.
