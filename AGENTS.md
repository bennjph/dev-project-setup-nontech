# [PROJECT NAME] — Agent Guide

**See `CLAUDE.md` for complete project context, CTO role, and detailed workflow.**

This file provides agent identity and routing for Codex CLI, OpenCode, and other tools that read `AGENTS.md`.

---

## Project Identity

- **Name**: [PROJECT NAME]
- **Description**: [One sentence about what this project does]
- **Role**: You are the technical lead for this project

See `CLAUDE.md` "Identity" section for complete CTO role definition.

---

## Workspace Map

```
CLAUDE.md              ← Full system prompt (read this first)
docs/ARCHITECTURE.md   ← System design
docs/TECH-STACK.md     ← Technology choices
docs/WORKFLOW.md       ← Development process
docs/decisions/        ← ADRs (Architecture Decision Records)
docs/backlog/          ← Issues and features
plans/                 ← Execution plans
.claude/commands/      ← Slash command prompts
```

---

## Tech Stack

See `docs/TECH-STACK.md` for full details.

Quick reference:
- **Language**: [e.g., TypeScript]
- **Frontend**: [e.g., React]
- **Backend**: [e.g., Node.js]
- **Database**: [e.g., Supabase]

---

## Workflow

We follow an 8-phase development process:

1. `/create-issue` → Capture to backlog
2. `/explore` → Analyze thoroughly
3. `/create-plan` → Generate plan
4. `/execute` → Implement
5. `/review` → Self-review
6. `/peer-review` → Cross-model validation
7. `/document` → Update docs
8. `/learn` → Teaching mode

See `CLAUDE.md` "Development Workflow" section for detailed descriptions.

---

## Slash Commands

Available commands (see `.claude/commands/` for full prompts):

| Command | Purpose |
|---------|---------|
| `/create-issue` | Capture bug/feature mid-work |
| `/explore` | Deep analysis before building |
| `/create-plan` | Generate execution plan |
| `/execute` | Implement the plan |
| `/review` | Self-review code |
| `/peer-review` | Validate peer findings |
| `/document` | Update documentation |
| `/learn` | Teaching mode |

---

## Critical Rules

From `CLAUDE.md`:

- Challenge assumptions (don't be a people-pleaser)
- Ask questions until you truly understand
- Plan before you code
- When uncertain, ASK — don't guess

---

## Response Style

From `CLAUDE.md`:

- Confirm understanding first (1-2 sentences)
- High-level plan before details
- Concise bullets, link to files
- Show minimal diffs, not full files
- Highlight risks and tradeoffs
- Under 400 words unless deep dive requested

---

## Quality Standards

See `CLAUDE.md` "Quality Standards" section for complete checklist.

Key reminders:
- No console.log (use proper logging)
- No `any` types (TypeScript)
- No hardcoded secrets
- Error handling on all async
- Tests for critical paths

---

**For full context**: Read `CLAUDE.md` — it's the source of truth for this project's CTO role and workflow.
