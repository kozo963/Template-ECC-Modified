# Failure & Rescue Policy

Applies to every task in the coder → reviewer loop.

## The ladder (per task)

| Attempt | Mode |
|---|---|
| 1–2 | Coder's own knowledge. NO internet. |
| 3–4 | Internet rescue: coder hands off to `explorer` with the EXACT error text, stack trace, and files involved. Coder reads findings and retries. |
| 5 | `ESCALATE: brain`. Coder stops and writes a FAIL report. |

Max 5 attempts per task. The counter resets only when the reviewer reports a DIFFERENT class of failure than the previous round.

## Explorer (internet rescue)

- Search the exact error message in quotes + framework + version (e.g. `"useEffect infinite loop" react 19`).
- Tool order: WebSearch / WebFetch. If a browser MCP (e.g. lightpanda) is wired, use it for pages that block fetching.
- Source order: official docs → GitHub issues → Stack Overflow.
- Version-check every suggestion against `rules/my-stack.md` (React 19, Vite 8, TS 7, Tailwind 4, supabase-js 2.x, react-router-dom 7). Discard answers written for older majors.
- Return 3–5 bullets + source URLs. No code.

## Coder FAIL report (required at attempt 5)

```
ESCALATE: brain
TASK: <milestone/task id>
ERROR: <exact message>
TRIED: 1) ... 2) ... 3) ...
FILES: <paths involved>
```

## Brain escalation

1. Read the FAIL report + reviewer feedback + explorer findings.
2. Implement the fix YOURSELF — the only case where the brain writes code.
3. If it passes review → append ONE line to `datasets/coder-failures.jsonl` (format in `datasets/README.md`). This is the fine-tuning set: what the coder didn't know.
4. If the brain also fails → mark the task `- [!]` BLOCKED in the milestone file with a one-line reason and surface it to the user.

## Dataset line (JSONL, one object per line)

```json
{"ts":"2026-08-28","milestone":"01-M-LandingPage","task":"T2","error":"...","tried":["...","..."],"solution":"...","lesson":"...","tags":["react19","tailwind4"]}
```
