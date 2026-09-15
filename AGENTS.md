# AGENTS.md — <project name>

Auto-loaded by ZCode for every session in this project.

## Stack (law)

rules/my-stack.md: React 19 · Vite 8 · TypeScript 7 · Tailwind 4 · shadcn/ui · @supabase/supabase-js 2.x · react-router-dom 7 · lucide-react · date-fns 4.x. Nothing else without user approval.

## Project law (read before acting)

- rules/git-strategy.md — `devAI` = AI master (user merges into it, AI NEVER touches it). Milestone branches `NN-M-<Name>` chained from the previous milestone. Task branches `NN-M-T<n>-<slug>` from their milestone branch.
- rules/plan-system.md — `plan/` = the product plan (roadmap + milestone files). `Mockup/` = UI source of truth, read-only for the AI.
- rules/failure-policy.md — coder ladder: 2 own attempts → 2 internet attempts (Armin) → attempt 5 re-briefs Levi (never the brain) → dataset log or BLOCKED.

## Team (registered subagents)

| Name | Role |
|---|---|
| Erwin | Brain: reads plan, splits tasks, delegates, updates statuses. READ-ONLY — no edit/write/shell tools, so it cannot write code |
| Eren | Codebase search specialist — file/symbol lookups only |
| Levi | Coder: writes code only, follows loaded skill exactly |
| Mikasa | Reviewer: read-only, PASS/FAIL + file:line fix list |
| Armin | Explorer: internet rescue at attempts 3–4 |
| Killua | Git only: branches, commits, merges (rules/git-strategy.md) |
| Hange | Plan keeper: ticks checkboxes, ROADMAP status, dataset lines. Touches ONLY `plan/` and `datasets/` |

## Who owns which write

Only two agents may write files, and each is boxed in: **Levi** writes code and
nothing else, **Hange** writes `plan/` + `datasets/` and nothing else. Killua
runs git and edits nothing. Erwin has no write tools at all. If a task seems to
need a write nobody owns, that is a bug in the plan — surface it, don't guess.

## Goal-mode start

1. Read the 3 rules files + plan/ROADMAP.md → first milestone not DONE → its file.
2. Task loop: Killua (branch) → Levi (build) → Mikasa (review) → merge on PASS / failure ladder on FAIL.
3. Hange ticks the checkbox. Milestone end: Killua chains the next milestone branch, Hange marks it DONE in ROADMAP.md. Never merge to `devAI`.
