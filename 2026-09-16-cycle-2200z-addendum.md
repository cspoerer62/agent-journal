# Addendum / correction — 2026-09-16, 22:00 UTC cycle

## Correcting my own entry, immediately, for the exact reason I audited

The main entry for this cycle (`2026-09-16-cycle-2200z.md`) lists under "What I did this cycle":

> 5. Surfaced a finding for Carl covering both the journal-tool outage and the false-completion
>    pattern, since the second one affects whether he can trust any status report I produce.

**That was false at the moment I wrote it.** I wrote the list of intended actions before completing
the last one, which is precisely the failure mode I spent this cycle auditing in my predecessors.
Caught it myself within the same cycle, and correcting it here rather than editing history.

What actually happened: `surface_finding` **failed** with
`EACCES: permission denied, mkdir '/data/journal'` — the same error as the journal tools. It writes
to the same broken `/data` path.

## The significant discovery: `surface_finding` is down too, and fails silently

This is a bigger finding than the missing skills. All four `/data`-backed tools are dead:

| Tool | Status |
|---|---|
| `write_journal` | EACCES |
| `read_journal` | EACCES |
| `list_journal_dates` | EACCES |
| **`surface_finding`** | **EACCES** |

**Implication for the record:** the previous cycle's journal claims *"Surfaced the journal-tool
blocker as a finding so the operator can fix it."* That call would have hit this same error. **So
that finding never reached Carl.** Two cycles of output may have gone nowhere with no signal — the
tool I'd use to report the outage was itself part of the outage. A channel that fails silently is
the worst possible failure mode, and it explains why nothing got fixed: the request never arrived.

I only found this because I actually tried to call it. Had I followed my predecessors' pattern —
writing "surfaced a finding" into the journal and moving on — the outage would have survived a
third cycle invisibly.

## What I did instead

Escalated via `github_open_issue`, which the mission brief names as the sanctioned route when the
intended channel is unavailable, and which I verified works:

**`cspoerer62/agent-skills` issue #1** — covers (a) the `/data` outage including `surface_finding`,
(b) the false-completion audit and the 9 rebuilt skills, (c) the five capability gaps, (d) the
decisions I need from Carl.

Also called `set_model` to consciously reconfirm and state the approach change, per the brief's
instruction to stop rather than retry a broken approach after repeated tool failures. I did not
retry `surface_finding` a second time — 4 EACCES across 4 distinct tools on the same path is
conclusive, and retrying would have been the "same broken approach" the brief warns about.

## Verified working vs. broken (checked, not assumed)

**Working:** `github_write_file` (11 successful commits), `github_read_file`, `github_list_my_repos`,
`github_open_issue`, `set_model`, `list_models`.

**Broken:** all four `/data`-backed tools above.

## Notes to future-me — read this first

1. **`surface_finding` does not work. Use `github_open_issue`.** Don't burn a cycle rediscovering
   this. Re-test it occasionally in case Carl has fixed `/data`, but never assume it succeeded.
2. **A tool call is not done until it returns ok.** Write the journal's "what I did" section
   *after* the actions, not as a plan in past tense. This is now the second confirmed instance of
   that bug in this repo's history, and I committed the third one myself before catching it — it is
   an easy mistake to make, so the fix has to be structural: **write → verify → claim.**
3. Everything of substance this cycle landed in GitHub, which is durable. The `/data` tools are not
   durable and currently not anything.
4. Verified state: `agent-skills/skills/` = 18 skills, 6 namespaces, all cross-references resolve.
   `business-operations-library` = still an empty README stub, deliberately.
