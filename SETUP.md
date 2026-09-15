# SETUP — from zero to first goal run

Give this file to whoever receives the template. Three parts: one-time
machine setup, per-project setup, first run.

## 0. What you are installing (30 seconds)

- **8 registered subagents** — real workers ZCode can spawn. They live in
  your HOME folder and work in every project. Each can have its own LLM.
- **19 agent docs** (in `agents/` of every project) — job descriptions the
  8 workers read and follow at the right moment. They are NEVER registered.

Rule: workers = global install once. docs = copied per project, never registered.

## Part A — one-time: install the 8 subagents (global)

Create these files in `C:\Users\<you>\.zcode\agents\` (macOS/Linux: `~/.zcode/agents/`).
For most of them, copy the matching file from this template's `agents/` folder and
ADD a frontmatter block on top (example below). Erwin, Eren and Hange differ — see
the notes under the table.

| Copy this template file | → save as | Name | Color | Role |
|---|---|---|---|---|
| `agents/brain.md` | `erwin.md` | Erwin | yellow | Brain: plans, delegates, updates statuses. READ-ONLY (see table note) |
| `agents/coder.md` | `levi.md` | Levi | red | Coder: writes code only |
| `agents/reviewer.md` | `mikasa.md` | Mikasa | orange | Reviewer: read-only, PASS/FAIL |
| `agents/explorer.md` | `armin.md` | Armin | cyan | Internet search (Lightpanda/WebSearch), read-only |
| `agents/git-agent.md` | `killua.md` | Killua | blue | Git only: branches, commits, merges |
| (content below) | `eren.md` | Eren | green | Codebase search only, read-only |
| `agents/plan-keeper.md` | `hange.md` | Hange | pink | Plan/dataset files only — checkboxes, ROADMAP status, dataset lines |
| `agents/visuals.md` | `hisoka.md` | Hisoka | purple | Blender/Unity/UI: builds and screenshot-verifies visuals |

**Colors must be one of** `red, blue, green, yellow, purple, orange, pink, cyan`.
Anything else is silently dropped, so the agent loses its colour chip.

Erwin is the one agent whose frontmatter is not optional boilerplate — the
`tools:` line is what makes the whole system work:

```markdown
---
name: "Erwin"
description: "The orchestrator. Use for planning, splitting tasks, delegating work, and driving a multi-step project to completion. Strictly read-only: it has no edit, write, or shell tools, so it CANNOT write code, run git, or touch files. It delegates every step — Levi (code), Killua (git), Mikasa (review), Eren (codebase search), Armin (internet), Hange (plan bookkeeping), Hisoka (visuals)."
color: yellow
injectAgentsMd: true
tools: [Read, Glob, Agent, TodoWrite]
---
```

`tools:` is an allowlist. Because it omits `Edit`, `Write` and `Bash`, Erwin
physically cannot do the work itself — delegation stops being a hint and becomes
the only path. The description is also load-bearing, not decoration: it is the
only string ZCode shows the model when choosing an agent, so write every
description as a firing rule ("Use PROACTIVELY when…"), never as a job title.

`eren.md` — paste as-is:

```markdown
---
name: "Eren"
description: "Use PROACTIVELY for any codebase search — locating files, symbols, definitions, call sites or usages, and answering 'where does X live / who calls X'. Returns file:line. Read-only. Not for internet lookups — that is Armin."
color: green
injectAgentsMd: true
---

You search the CODEBASE only. Never the internet (that is Armin's job).

## Rules
- Find files, symbols, usages, definitions — report file paths + line numbers.
- Summarize findings in 3-5 bullets. No code changes. Read-only.
```

`hange.md` — paste as-is:

```markdown
---
name: "Hange"
description: "Use whenever plan or dataset bookkeeping is required — ticking a task checkbox in a plan/ milestone file, updating plan/ROADMAP.md status, splitting an oversized task into subtasks, writing a `- [!]` BLOCKED marker, or appending a line to datasets/coder-failures.jsonl. Touches ONLY plan/ and datasets/. Never source code, never git, never builds."
color: pink
injectAgentsMd: true
tools: [Read, Glob, Grep, Edit, Write]
---
```

then the body of `agents/plan-keeper.md`.

`hisoka.md` — paste as-is:

```markdown
---
name: "Hisoka"
description: "Use PROACTIVELY for all visual work: Blender modeling/materials/lighting/scene/VFX, Unity scene and visual setup, and building or restyling web/app UI with screenshot verification. Always plans first in a markdown checklist. Not for gameplay, business logic, backend or data code — that is Levi."
color: purple
injectAgentsMd: true
---
```

then the body of `agents/visuals.md`.

Optional: pin a model per worker by adding `model: "<model-id>"` in the
frontmatter (e.g. a cheap local model for Eren/Killua, a strong one for Erwin).
No `model:` line = your default model. Avoid `model: "inherit"` on Erwin — it
would run every orchestration turn at your main session's cost.

Restart ZCode. Settings → Subagents must now show 8 agents. Do NOT register
the other 19 files from `agents/` — the workers load them from disk on demand.

## Part B — per project: install the template

Copy the template CONTENTS into the new project's ROOT (do not rename anything,
do not put it inside `.zcode/`):

```
my-app/
├── AGENTS.md          ← the ONLY file ZCode auto-loads every session
├── SKILLS-INDEX.md
├── agents/            ← 19 docs (already copied with the folder)
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

1. Restart ZCode, confirm the 8 subagents exist.
2. Open the project, start goal mode with something like:
   `Work plan/01-M-LandingPage.md task T1 following AGENTS.md.`
   (or run `/delegate task T1 of plan/01-M-LandingPage.md`)
3. Expected loop: Erwin reads the plan → Killua creates the task branch →
   Levi builds (matching the mockup) → Mikasa reviews → FAIL: retry ladder
   (2 own attempts → 2 with Armin on the internet → attempt 5 re-briefs Levi,
   never Erwin) → PASS: Killua merges → Hange ticks the checkbox.

The signature of a working install: **no file ever changes that wasn't changed
by Levi, Killua or Hange.** If Erwin edits something, its `tools:` allowlist is
missing or wrong.

## Verification checklist

- [ ] 8 agents visible in Settings → Subagents
- [ ] Erwin's frontmatter contains `tools: [Read, Glob, Agent, TodoWrite]`
- [ ] `AGENTS.md` exists in the project root
- [ ] `plan/ROADMAP.md` has at least one milestone with status TODO
- [ ] Every task line points to an existing Mockup path (or says "no mockup")
- [ ] `git branch` shows `devAI`
- [ ] After the first task: task branch merged into `01-M-...`, checkbox ticked
