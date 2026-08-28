
**Result:** 300 tokens instead of 15,000. The other 67 agents cost zero.

### Why this template, not the full ECC?

| Full ECC | This Template |
|---|---|
| 68 agents | 17 agents (12 from ECC + 5 personas) |
| 286 skills | 11 skills |
| All languages | Only React/TypeScript/Supabase stack |
| Requires Claude Code | Works with zCode GOAL MODE |
| Cloud-first | Local-first with optional cloud brain |

---

## 3. What Was Selected and Why

### Agents from ECC (12 files)

| Agent | Why Selected |
|---|---|
| `planner.md` | Core orchestrator. Breaks tasks into steps. |
| `code-reviewer.md` | General code quality review. |
| `react-reviewer.md` | React-specific review (hooks, JSX, boundaries). |
| `typescript-reviewer.md` | TypeScript type safety and patterns. |
| `build-error-resolver.md` | Fixes build/compile failures automatically. |
| `security-reviewer.md` | OWASP-style security audit before deploy. |
| `database-reviewer.md` | Reviews SQL and Supabase queries. |
| `e2e-runner.md` | Runs end-to-end user flow tests. |
| `doc-updater.md` | Keeps documentation in sync with code. |
| `performance-optimizer.md` | Fixes slow renders and bundle size. |
| `refactor-cleaner.md` | Removes dead code and simplifies. |
| `tdd-guide.md` | Enforces test-driven development workflow. |

### Agents NOT selected (and why)

| Agent | Why Skipped |
|---|---|
| `gan-evaluator.md` | Only for GAN/ML projects. Not relevant. |
| `healthcare-reviewer.md` | Domain-specific. Not needed. |
| `homelab-architect.md` | Infrastructure. Not relevant. |
| `cpp-reviewer.md` | Wrong language. |
| `rust-reviewer.md` | Wrong language. |
| `go-reviewer.md` | Wrong language. |
| `python-reviewer.md` | Not in current stack. Add later if needed. |
| `java-reviewer.md` | Not in current stack. Add later if needed. |
| `csharp-reviewer.md` | Not in current stack. Add later if needed. |

### Custom Personas (5 files)

These are NEW agents we wrote. They do not exist in ECC.

| Persona | Purpose |
|---|---|
| `brain.md` | Orchestrator. Reads index, delegates. Never writes code. |
| `coder.md` | Writes code. Follows loaded skill exactly. |
| `reviewer.md` | Checks code against rules. Outputs PASS/FAIL. |
| `git-agent.md` | Runs git commands only. No code changes. |
| `explorer.md` | Searches internet for docs and error solutions. |

### Skills from ECC (11 files)

| Skill | Why Selected |
|---|---|
| `tdd-workflow` | Core workflow. Forces test-first development. |
| `react-patterns` | React 18/19 idioms and best practices. |
| `react-testing` | React Testing Library + Vitest patterns. |
| `react-performance` | 70-rule performance ruleset from Vercel Labs. |
| `typescript-patterns` | TypeScript type design and patterns. |
| `backend-patterns` | API and backend design patterns. |
| `security-review` | Security audit checklist. |
| `e2e-testing` | End-to-end testing workflow. |
| `git-workflow` | Git branching and commit conventions. |
| `coding-standards` | Universal coding style rules. |
| `sql-patterns` | Database query best practices. |

### Rules from ECC (3 directories)

| Directory | Contents | Why |
|---|---|---|
| `common/` | Universal rules (style, security, testing) | Applies to all projects |
| `react/` | React-specific rules (hooks, patterns, security) | Your primary framework |
| `typescript/` | TypeScript-specific rules | Your primary language |

### Custom Rule (1 file)

| File | Purpose |
|---|---|
| `my-stack.md` | Your exact stack: React 19 + Vite + Supabase + shadcn/ui |

---

## 4. The Execution Loop

This is the core workflow. Every task follows this pipeline.
