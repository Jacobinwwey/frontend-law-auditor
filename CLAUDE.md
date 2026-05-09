# CLAUDE.md

This file gives coding-agent guidance for this repository.

## Project Overview

`frontend-law-auditor` is a standalone skill repo with:
- `SKILL.md` for agent behavior and output contract
- `scripts/law_audit.py` for metric-based gating and reporting
- `rules/` and `references/` for principle-level diagnosis playbooks

## Key Commands

```bash
# Generate evidence template
python scripts/law_audit.py --init-template ./examples/evidence.local.json

# Run markdown + JSON audit outputs
python scripts/law_audit.py \
  --input ./examples/evidence.local.json \
  --output ./examples/audit.local.md \
  --json-out ./examples/audit.local.json

# Strict CI gate
python scripts/law_audit.py \
  --input ./examples/evidence.local.json \
  --strict \
  --fail-threshold 85
```

## Architecture Notes

- The Python script is dependency-light (stdlib only) to keep runtime portable.
- Rule documents are mapped from principle keys in `RULE_FILE_MAP`.
- Strict mode returns non-zero if any fast-gate check fails or overall score is below threshold.
