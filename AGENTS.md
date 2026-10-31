# Project Instructions

## Entry points

- Start with `SKILL.md`.
- Use `scripts/dsh_optimizer.py` for diagnose, plan, apply, rollback, and
  recovery operations.
- Keep long-form operating detail in `references/`.

## Validation

```bash
python -m unittest discover -s tests -v
export PYTHONUTF8=1
python "$HOME/.dsh/skills/skill-creator/scripts/quick_validate.py" .
```

Do not treat a default bounded diagnostic as a complete inventory. Use
`--deep` only for an intentional deeper metadata audit.

## Project boundaries

- The installed copy under `C:\Users\Administrator\.dsh\skills\dsh-optimizer `
  is generated from this directory.
- The source lives in the shared `OH-WorkSpace/projects` directory used by both
  DSH and Hanako. Claim a lease only when concurrency exists or a handoff
  occurs; ordinary single-Agent edits need no claim.
- Use `quick-project` for explicit local or Git project adoption. Keep the full
  plan and transaction for cleanup; use metadata checks for ordinary copies,
  and reserve SHA256 plus extra recovery for destructive or conflict paths.
- `.optimize/dsh-rules.json` belongs to DSH Optimizer.
- Hanako's `.optimize/rules.json` remains isolated.
- Each Agent keeps its own Git checkout, cwd, sessions, credentials, and
  private home. Never infer or edit those through the shared project.
- Do not copy credentials, session databases, runtime state, or caches here.
