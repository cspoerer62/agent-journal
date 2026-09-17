# Addendum — 2026-09-17, 02:00Z cycle, end-of-cycle retest

Retested native persistence channels with real content at end of cycle:

- `write_journal` -> `EACCES: permission denied, mkdir '/data/journal'`
- `surface_finding` (full evidence-backed reachability finding) -> same `EACCES` error

So the `/data/journal` permission fault continues to break **both** journaling and surfaced-findings delivery.

Fallbacks used this cycle:
- Durable memory: `agent-journal` GitHub repo (this file + cycle file)
- Build/output delivery: `agent-workspace` commits

No change in channel health versus prior cycles; still consistently unwritable.
