# CLAUDE.md

This file gives coding-agent guidance for this repository.

## Project Overview

`frontend-law-auditor` is a standalone skill repo with:
- `SKILL.md` as the canonical workflow and output contract
- `skills/frontend-law-auditor/SKILL.md` as the packaged Codex skill entrypoint
- `.claude/skills/frontend-law-auditor/SKILL.md` as the packaged Claude entrypoint
- `.codex/INSTALL.md`, `.codex-plugin/plugin.json`, `.opencode/INSTALL.md`, and `.cursorrules` as agent bootstrap/package surfaces
- `scripts/law_audit.py` for metric-based gating and reporting
- `rules/` and `references/` for principle-level diagnosis playbooks

## Key Commands

```bash
# Generate evidence template
python3 scripts/law_audit.py --init-template ./examples/evidence.local.json

# Run markdown + JSON audit outputs
python3 scripts/law_audit.py \
  --input ./examples/evidence.local.json \
  --output ./examples/audit.local.md \
  --json-out ./examples/audit.local.json

# Strict CI gate
python3 scripts/law_audit.py \
  --input ./examples/evidence.local.json \
  --strict \
  --fail-threshold 85
```

## Architecture Notes

- The Python script is dependency-light (stdlib only) to keep runtime portable.
- Rule documents are mapped from principle keys in `RULE_FILE_MAP`.
- Strict mode returns non-zero if any fast-gate check fails or overall score is below threshold.
- Keep the root `SKILL.md`, `skills/frontend-law-auditor/SKILL.md`, and `.claude/skills/frontend-law-auditor/SKILL.md` aligned when changing workflow instructions.
- The install-facing metadata lives in `skill.json`, `.codex-plugin/plugin.json`, `.claude-plugin/plugin.json`, and `.claude-plugin/marketplace.json`.
