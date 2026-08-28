# Plan System (where the Brain reads the app plan)

The Brain NEVER invents the product plan. It reads it from `plan/`.
The user writes the high level (milestones + tasks). The Brain splits big
tasks into subtasks. Mockups are the single source of truth for UI.

## Folder layout (project root)

```
plan/
  ROADMAP.md                    <- all milestones, one line each (USER writes)
  01-M-LandingPage.md           <- one file per milestone (USER writes tasks, Brain extends)
  _templates/                   <- copy these when creating a new milestone
Mockup/                          <- user's HTML wireframes (NOT inside plan/)
  01-M-LandingPage/
    landingPage.html
    LoginPage.html
  Data/
    Logo.svg                     <- shared assets, always referenced by exact path
```

## Naming

- Milestone: `NN-M-<Name>` (e.g. `01-M-LandingPage`). File: `plan/NN-M-<Name>.md`. Branch: same name.
- Task: `T1-<short title>` inside the milestone file. Subtask: `T1.1`, `T1.2`, ...
- Mockups for milestone `NN` live in `Mockup/NN-M-<Name>/`. A task MUST reference its mockup by exact relative path.
- Shared assets live in `Mockup/Data/` and are referenced by path (`Mockup/Data/Logo.svg`).

## Brain duties per milestone

1. Read `plan/ROADMAP.md` → take the first milestone without status DONE → read its file.
2. For each TODO task: if it is too big for one coder run (touches > ~3 files, or mixes UI + logic + database), split it into subtasks `T1.1, T1.2, ...` and WRITE them back into the milestone file under the parent task. Never hand an unsplit mega-task to the coder.
3. Run each task/subtask through the loop: Killua (task branch) → coder (build) → reviewer (PASS/FAIL) → Killua (merge on PASS). Failure handling: rules/failure-policy.md.
4. After every task, tick its checkbox in the milestone file.
5. When no boxes remain and the build is green: tell git-agent to chain the next milestone branch, then mark the milestone DONE in `plan/ROADMAP.md`.

## How the user writes tasks (milestone file, Tasks section)

```
- [ ] T1-Create the Landing page — UI: Mockup/01-M-LandingPage/landingPage.html
- [ ] T2-Create the LogInPage and connect it to the CTA button on the landing page — UI: Mockup/01-M-LandingPage/LoginPage.html
- [ ] T3-Use Mockup/Data/Logo.svg as the logo in every slot that shows a logo
```

A good task: one deliverable · names its mockup path · names what it connects to.
Done means: reviewer PASS + `npm run build` green + mockup matched.

## Status vocabulary

Task: `- [ ]` TODO → `- [x]` done → `- [!]` BLOCKED (append one-line reason).
Milestone (ROADMAP.md): TODO → IN PROGRESS → DONE → BLOCKED.
