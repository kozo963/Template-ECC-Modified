# SETUP — from zero to first goal run

Give this file to whoever receives the template. Three parts: one-time
machine setup, per-project setup, first run.

## 0. What you are installing (30 seconds)

- **6 registered subagents** — real workers ZCode can spawn. They live in
  your HOME folder and work in every project. Each can have its own LLM.
- **17 agent docs** (in `agents/` of every project) — job descriptions the
  6 workers read and follow at the right moment. They are NEVER registered.

Rule: workers = global install once. docs = copied per project, never registered.

## Part A — one-time: install the 6 subagents (global)

Create these files in `C:\Users\<you>\.zcode\agents\` (macOS/Linux: `~/.zcode/agents/`).
For 5 of them, copy the matching file from this template's `agents/` folder and
ADD a frontmatter block on top (example below). The 6th (Eren) is given in full.

| Copy this template file | → save as | Name | Color | Role |
|---|---|---|---|---|
| `agents/brain.md` | `erwin.md` | Erwin | yellow | Brain: plans, delegates, updates plan, escalation fixes |
| `agents/coder.md` | `levi.md` | Levi | red | Coder: writes code only |
| `agents/reviewer.md` | `mikasa.md` | Mikasa | orange | Reviewer: read-only, PASS/FAIL |
| `agents/explorer.md` | `armin.md` | Armin | cyan | Internet search (Lightpanda/WebSearch), read-only |
| `agents/git-agent.md` | `killua.md` | Killua | gray | Git only: branches, commits, merges |
| (content below) | `eren.md` | Eren | green | Codebase search only, read-only |

Frontmatter format (goes on line 1 of each file):

```markdown
---
name: "Erwin"
description: "The main brain. Plans, branches, delegates, and merges."
color: yellow
injectAgentsMd: true
---
```

`eren.md` — paste as-is:

```markdown
---
name: "Eren"
description: "Codebase search specialist. Read-only. Never writes code."
color: green
injectAgentsMd: true
---

You search the CODEBASE only. Never the internet (that is Armin's job).

## Rules
- Find files, symbols, usages, definitions — report file paths + line numbers.
- Summarize findings in 3-5 bullets. No code changes. Read-only.
```

Optional: pin a model per worker by adding `model: "<model-id>"` in the
frontmatter (e.g. a cheap local model for Eren/Killua, a strong one for Erwin).
No `model:` line = your default model.

Restart ZCode. Settings → Subagents must now show 6 agents. Do NOT register
the other 17 files from `agents/` — the workers load them from disk on demand.

## Part B — per project: install the template

Copy the template CONTENTS into the new project's ROOT (do not rename anything,
do not put it inside `.zcode/`):

```
my-app/
├── AGENTS.md          ← the ONLY file ZCode auto-loads every session
├── SKILLS-INDEX.md
├── agents/            ← 17 docs (already copied with the folder)
├── rules/             ← law: my-stack, git-strategy, plan-system, failure-policy
├── skills/            ← 11 docs, loaded on demand
├── datasets/          ← coder-failures.jsonl (fine-tuning harvest)
├── plan/              ← YOU fill this (Part C)
└── Mockup/            ← YOU fill this (Part C)
```

## Part C — per project: what YOU write

1. `plan/ROADMAP.md` — one line per milestone: `| 01 | LandingPage | plan/01-M-LandingPage.md | TODO |`
2. One milestone file per milestone, copied from `plan/_templates/milestone.md`:
   `plan/01-M-LandingPage.md`. Write tasks in this format:

```
- [ ] T1-Create the Landing page — UI: Mockup/01-M-LandingPage/landingPage.html
- [ ] T2-Create the LogInPage, connect it to the CTA on the landing page — UI: Mockup/01-M-LandingPage/LoginPage.html
- [ ] T3-Use Mockup/Data/Logo.svg as the logo everywhere
```

3. `Mockup/NN-M-<Name>/` — one static HTML wireframe per page + shared assets
   in `Mockup/Data/` (e.g. `Logo.svg`). Static HTML only; the AI never edits it.
4. Check `rules/my-stack.md` matches your stack. If not, edit it — every agent
   obeys it.

## Part D — git init (one time per project)

```bash
git init
git checkout -b devAI        # the AI's master branch; YOU merge milestones into it
```

`main` is yours. The AI NEVER commits to `main` or `devAI` — it works in
milestone branches (`01-M-...`) and task branches (`01-M-T1-...`), and Killua
chains each milestone from the previous one. You merge milestone branches into
`devAI` yourself, in order — a broken milestone simply never reaches it.

## Part E — first run

1. Restart ZCode, confirm the 6 subagents exist.
2. Open the project, start goal mode with something like:
   `Work plan/01-M-LandingPage.md task T1 following AGENTS.md.`
3. Expected loop: Erwin reads the plan → Killua creates the task branch →
   Levi builds (matching the mockup) → Mikasa reviews → FAIL: retry ladder
   (2 own attempts → 2 with Armin on the internet → escalate to Erwin) →
   PASS: Killua merges → Erwin ticks the checkbox in the plan file.

## Verification checklist

- [ ] 6 agents visible in Settings → Subagents
- [ ] `AGENTS.md` exists in the project root
- [ ] `plan/ROADMAP.md` has at least one milestone with status TODO
- [ ] Every task line points to an existing Mockup path (or says "no mockup")
- [ ] `git branch` shows `devAI`
- [ ] After the first task: task branch merged into `01-M-...`, checkbox ticked
