# Failure & Rescue Policy

Applies to every task in the coder → reviewer loop.

## The ladder (per task)

| Attempt | Mode |
|---|---|
| 1–2 | Coder's own knowledge. NO internet. |
| 3–4 | Internet rescue: coder hands off to **Armin** with the EXACT error text, stack trace, and files involved. Coder reads findings and retries. |
| 5 | `ESCALATE: fresh-approach`. Coder stops and writes a FAIL report. |

Max 5 attempts per task. The counter resets only when the reviewer reports a DIFFERENT class of failure than the previous round.

**The brain never writes code.** Attempt 5 is a coder attempt, not a brain
attempt — the brain's job is to re-brief the coder with everything learned.

## Explorer (internet rescue)

- Search the exact error message in quotes + framework + version (e.g. `"useEffect infinite loop" react 19`).
- Tool order: WebSearch / WebFetch. If a browser MCP (e.g. lightpanda) is wired, use it for pages that block fetching.
- Source order: official docs → GitHub issues → Stack Overflow.
- Version-check every suggestion against `rules/my-stack.md` (React 19, Vite 8, TS 7, Tailwind 4, supabase-js 2.x, react-router-dom 7). Discard answers written for older majors.
- Return 3–5 bullets + source URLs. No code.

## Coder FAIL report (required at attempt 5)

```
ESCALATE: fresh-approach
TASK: <milestone/task id>
ERROR: <exact message>
TRIED: 1) ... 2) ... 3) ...
FILES: <paths involved>
```

## Brain escalation (attempt 5)

The brain is read-only. It has no edit or write tools, so fixing the code itself
is not an option it has — and not an option it should want. Instead:

1. Assemble the full brief: the FAIL report, every reviewer FAIL list, every
   attempt and its exact error, and Armin's findings.
2. Re-invoke **Levi** in a fresh call with that brief, requiring:
   - a stated root cause and a named different approach BEFORE any code;
   - no repetition of any approach listed as already tried;
   - a FAIL report immediately, with no guessing, if it cannot name a different
     hypothesis.
3. Does it pass Mikasa?
   - **Yes** → tell **Hange** to append ONE line to `datasets/coder-failures.jsonl`
     (format in `datasets/README.md`). This is the fine-tuning set: what the coder
     didn't know.
   - **No** → tell **Hange** to mark the task `- [!]` BLOCKED in the milestone
     file with a one-line concrete reason, then surface it to the user and stop.

Bookkeeping — the checkbox, the BLOCKED marker, the ROADMAP status, the dataset
line — belongs to **Hange**. The brain reads and decides; it never writes files.

## Dataset line (JSONL, one object per line)

```json
{"ts":"2026-08-28","milestone":"01-M-LandingPage","task":"T2","error":"...","tried":["...","..."],"solution":"...","lesson":"...","tags":["react19","tailwind4"]}
```
