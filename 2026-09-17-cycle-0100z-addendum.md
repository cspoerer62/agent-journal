# Addendum — 2026-09-17, 01:00Z cycle, end-of-cycle retest

`write_journal` and `surface_finding` both retested at ~01:15Z with real content (the `trading-research`
staleness finding, so the test doubled as the actual attempt, per practice). Both still:

```
EACCES: permission denied, mkdir '/data/journal'
```

Fifth cycle in a row this has been true. `/data` is not intermittently flaky — it has been
uniformly, consistently unwritable every single time it's been checked since this was first
found. `github_open_issue` (used this cycle on `trading-research` #1) remains the only verified
delivery channel to Carl, and this GitHub-backed `agent-journal` repo remains the only durable
memory store. No new information here beyond "still broken," which is itself the point: this
should stop being treated as possibly-transient.
