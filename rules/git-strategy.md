# Git Strategy (project law)

The AI's master branch is `devAI`. The user owns `main` and `devAI`.
The AI never merges anything into `devAI` — that is the user's quality gate.

## Branches

| Branch | Created by | Purpose |
|---|---|---|
| `main` | user | production. AI NEVER touches. |
| `devAI` | user | AI master. AI never commits directly. Only the user merges milestone branches into it. |
| `NN-M-<Name>` | Killua (git subagent) | one branch per milestone (e.g. `01-M-LandingPage`). |
| `NN-M-T<n>-<slug>` | Killua (git subagent) | one branch per task, created FROM its milestone branch. |

## Rules

1. NEVER commit to `devAI` or `main`.
2. Task branch merges into its milestone branch ONLY after reviewer PASS (`--no-ff`, keep task history).
3. On FAIL: fix on the SAME task branch, re-review. No new branch per retry.
4. Milestone complete (all tasks PASS + build green) → Killua creates the NEXT milestone branch FROM the current milestone branch. Milestones chain: 03 builds on 02 builds on 01.
5. A broken milestone simply never reaches `devAI` — the user merges milestone branches into `devAI` manually, in order. Nothing after the broken one gets merged either.
6. Commit scope encodes position: `<type>(M<NN>-T<n>): <subject>`, e.g. `feat(M01-T2): wire login form to landing CTA`.

## Command chain (example)

```bash
# milestone 01 (first milestone branches from devAI)
git checkout devAI && git checkout -b 01-M-LandingPage

# task branch
git checkout -b 01-M-T1-landing-page 01-M-LandingPage
# ... coder works, commits ...
git add . && git commit -m "feat(M01-T1): landing page from mockup"

# on reviewer PASS
git checkout 01-M-LandingPage
git merge --no-ff 01-M-T1-landing-page

# milestone 02 chains from milestone 01 (NOT from devAI)
git checkout -b 02-M-Auth 01-M-LandingPage
```
