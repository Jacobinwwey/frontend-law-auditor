---
name: frontend-law-auditor
description: Packaged Claude entrypoint for the Frontend Law Auditor skill. Use when reviewing a frontend for UX friction, measurable release gating, and law-based remediation planning.
license: Complete terms in ../../../LICENSE.txt
---

# Frontend Law Auditor

This packaged entrypoint mirrors the repository-root `SKILL.md` so Claude-compatible loaders have a stable skill path.

## Bootstrap Rules

1. Treat the repository root as `../../..`.
2. Read `../../../SKILL.md` before performing any audit.
3. Load supporting files only as needed:
   - `../../../references/metrics-schema.md`
   - `../../../references/theory-playbook.md`
   - `../../../rules/_sections.md`
   - `../../../rules/<law>.md`
   - `../../../examples/evidence.sample.json`
4. Use the bundled CLI from the repository root:

```bash
python3 ../../../scripts/law_audit.py --init-template /tmp/frontend-evidence.json
python3 ../../../scripts/law_audit.py --input /tmp/frontend-evidence.json --output /tmp/frontend-audit.md --json-out /tmp/frontend-audit.json
python3 ../../../scripts/law_audit.py --input /tmp/frontend-evidence.json --strict --fail-threshold 85
```

## Required Output

Every audit must still produce:

1. **Fast Gate Failures**
2. **Law Diagnosis**
3. **Priority Fix Plan**
4. **Recheck Checklist**

Never invent evidence. Missing metrics must remain `unknown`.
