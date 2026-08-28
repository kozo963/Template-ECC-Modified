# ZCode Agent Template System
> Based on ECC (Engineering Command Center) architecture.
> Adapted for zCode GOAL MODE, local Qwen models, and cost optimization.

---

## Table of Contents
1. [What Is This](#1-what-is-this)
2. [Why We Did It This Way](#2-why-we-did-it-this-way)
3. [What Was Selected and Why](#3-what-was-selected-and-why)
4. [The Execution Loop](#4-the-execution-loop)
5. [How GOAL MODE Uses This](#5-how-goal-mode-uses-this)
6. [File Structure](#6-file-structure)
7. [Agent Personas Explained](#7-agent-personas-explained)
8. [Your Stack Rules](#8-your-stack-rules)
9. [Cost Optimization Strategy](#9-cost-optimization-strategy)
10. [How to Extend](#10-how-to-extend)
11. [Quick Reference](#11-quick-reference)

---

## 1. What Is This

This is a **template system** for zCode that turns a single AI chat into a
coordinated engineering team. It is inspired by the ECC project
(github.com/affaan-m/ECC), which won the Anthropic x Forum Ventures
hackathon in September 2025.

Instead of asking one AI to do everything in one giant prompt, this system:

- **Plans** before it builds.
- **Tests** before it implements.
- **Reviews** its own work.
- **Commits** only when verified.
- **Remembers** what worked.

The core philosophy:

> Optimize the context window. Persist everything else.

---

## 2. Why We Did It This Way

### Why not download all 68 agents and 286 skills?

ECC ships with 68 agents and 286 skills. Loading all of them into context
at once would:

| Problem | Impact |
|---|---|
| Context overflow | 68 agent descriptions = ~15,000 tokens before any work starts |
| Model confusion | Small local models (7B/14B) cannot choose from 68 options reliably |
| Token waste | 90% of skills are irrelevant to any single task |
| Slow responses | More context = slower inference on local hardware |

### The Dispatcher Pattern (the solution)

We keep ALL agents and skills on disk. But the brain (orchestrator) reads
only ONE file: `SKILLS-INDEX.md`. This file is ~30 lines. The brain picks
the right agent, and the harness loads ONLY that agent's file into context.
