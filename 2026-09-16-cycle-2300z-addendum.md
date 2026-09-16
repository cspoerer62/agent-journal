# Addendum — 2026-09-16, 23:00Z cycle

## I did item 3 instead of leaving it to future-me

The main entry's "Notes to future-me" #4 said the last known dangling reference in the system was
that **every skill in `agent-skills` instructs the agent to output a `surface_finding`, which is a
dead channel**, and suggested a future cycle patch it.

Leaving a known dangling reference in place while writing a note asking someone else to fix it is
a weaker version of the exact bug this repo's audit was about. It took one commit. I did it.

**`agent-skills/README.md` → commit `2d4e7c5`.** Changes:

1. **New block near the top: "⚠️ Runtime channel status — read this before following any skill's
   escalation instruction."** States plainly that `surface_finding` is dead, that every skill's
   escalation instruction should be read as "open a GitHub issue," and gives the verified
   working/broken table with the date and the exact error.
2. **Corrected the "Honest capability statement."** It previously listed `journal` and
   `surface_finding` among the tools the agent *has*. That was true when written and is now false,
   and it was the most load-bearing false sentence in the repo — it's the section a reader consults
   specifically to find out what the agent can actually do. Added a row: "Report a finding to Carl
   → **Yes, but not via `surface_finding`** — via `github_open_issue`."
3. **Added §5 pointing at `docs/AUDIT-2026-09-16.md`**, so the audit isn't discoverable only by
   someone who already knows to look for it.
4. **Added a cross-link table to `business-operations-library`'s six runbooks**, so the skill layer
   and the operations layer reference each other in both directions rather than only one way.
5. **Added the verification date and per-namespace counts** to the 18-skill list ("verified present
   by directory listing on 2026-09-16 23:00Z; business 4, sales 3, research 3, design 2, media 2,
   thinking 4"). A count with a verification date is a different kind of claim than a bare count —
   and a bare count is precisely what was wrong before.
6. Changed the `thinking/evidence-grading` row from "the anti-bullshit layer under `surface_finding`"
   to "...under any finding," since the tool it named no longer works.

Verified by reading the file back at the commit hash `2d4e7c5` in a separate call after the write.

## Final verified state of this cycle

| Artifact | State | How verified |
|---|---|---|
| `business-operations-library` 6 runbooks + README index | **Built** | Repo root + all 4 subdirs re-listed in separate calls |
| `business-operations-library` issue #1 | **Open** — build report + the two decisions needed from Carl | Tool returned `ok`, issue number 1 |
| `agent-journal/2026-09-16-cycle-2300z.md` | **Written** | Directory re-listed, file present |
| `agent-skills/README.md` channel-status patch | **Written** | Read back at commit `2d4e7c5` |
| `surface_finding` | **Still broken** | Called with real content at end of cycle; `EACCES` |

## The one thing I'd flag to the next cycle above all else

**Stop writing doctrine.** Six runbooks, 18 skills, a registry of ~160 upstream skills, an audit,
and a decision log now exist. Not one of them has ever been executed against a real business fact.
The `log/` and `close/` directories are empty and the README says so.

The next unit of value is not a seventh document. It is either:
- **Carl populates ~20 rows of the master register** (blocking: the close's charge-matching check,
  Station 4's diff, and the single-point-of-failure list), or
- **I execute one real weekly run** against whatever genuinely exists — even if the honest output
  is six stations reporting "no properties, no pipeline, no accounts registered" — because a real
  log with honest UNKNOWNs is worth more than another template, and it would immediately reveal
  which parts of the checklist are unexecutable as written.

Both are named in issue #1 with cost-of-delay attached. If the issue is still unanswered next
cycle, do the second one — it needs nothing from anyone.
