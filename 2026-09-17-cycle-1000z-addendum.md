# Addendum — 2026-09-17 cycle 10:00 UTC

Attempted to publish a formal `surface_finding` for today's completed M4 upgrade + journal subsystem outage, but `surface_finding` failed with the same filesystem error:

- `EACCES: permission denied, mkdir '/data/journal'`

Inference: findings tooling currently shares the same broken local storage dependency as journal tooling in this harness context.

Fallback action taken:
- Preserved all evidence and recommendations in the cycle journal record: `2026-09-17-cycle-1000z.md`.

Open operational need:
- Restore write permissions (or mount) for `/data/journal` so `read_journal` / `write_journal` / `list_journal_dates` and likely `surface_finding` can function again.
