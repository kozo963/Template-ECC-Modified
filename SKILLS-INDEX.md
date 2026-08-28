# Agent & Skill Index

The brain reads ONLY this file. Do NOT load all agents.

## Personas (the pipeline)
| Agent | Load When |
|---|---|
| coder | Building or fixing a task |
| reviewer | After every coder output |
| git-agent | Branch/merge operations only |
| explorer | Internet rescue (coder attempts 3-4) |

## Specialists (from ECC)
| Agent | Load When |
|---|---|
| planner | Designing a new feature before tasks are written |
| tdd-guide | Writing code with tests first |
| code-reviewer | Deep code quality review |
| react-reviewer | Reviewing React/TSX components |
| typescript-reviewer | Reviewing TypeScript types/logic |
| build-error-resolver | Build or compile fails |
| security-reviewer | Before deploying to production |
| database-reviewer | Writing SQL or Supabase queries |
| e2e-runner | Running end-to-end tests |
| performance-optimizer | Optimizing slow components |
| doc-updater | Updating documentation |
| refactor-cleaner | Removing dead code |

## Skills
| Skill | Use When |
|---|---|
| tdd-workflow | Writing new code or fixing bugs |
| react-patterns | Building React components |
| react-testing | Writing React tests |
| react-performance | Fixing slow React renders |
| typescript-patterns | TypeScript type design |
| security-review | Checking for vulnerabilities |
| e2e-testing | Testing full user flows |
| git-workflow | Committing, branching, merging |
| sql-patterns | Writing database queries |

## Project law (brain reads at goal start — not "loaded", just read)
- rules/plan-system.md — plan/ + Mockup/ layout, how tasks are split
- rules/failure-policy.md — retry ladder, internet rescue, escalation, dataset log
- rules/git-strategy.md — devAI / milestone / task branch law
