# Update Documentation

Update project documentation after code changes.

---

## Mission

Keep documentation in sync with the actual codebase.

**Critical rule**: Do NOT trust existing documentation. Read the actual code to verify current implementation.

---

## Process

### Step 1: Identify Changes

What just changed?

- Check recent commits (if using git)
- Read the active plan in `plans/`
- Ask user which files were modified

### Step 2: Verify Current Implementation

**Do NOT assume** — read the actual code:

- What does the code ACTUALLY do?
- What patterns are ACTUALLY used?
- What dependencies are ACTUALLY installed?

**Avoid**: Copying old docs or guessing based on what "should" be there.

### Step 3: Update Relevant Documentation

Check which docs need updating:

#### `docs/ARCHITECTURE.md`

Update if:
- System design changed (new components, services, flows)
- Data model changed (new entities, relationships)
- Critical areas changed (authentication, payments, etc.)

What to update:
```markdown
## Overview
[Update if overall architecture changed]

## System Diagram
[Update if components added/removed]

## Key Components
- **[New Component]**: [What it does, where it lives]

## Data Model
[Update if database schema changed]

## Critical Areas
- `path/to/sensitive/` — [Update if new sensitive areas added]
```

#### `docs/TECH-STACK.md`

Update if:
- New dependencies added (`package.json` changed)
- Framework/library versions upgraded
- Infrastructure changes (hosting, database, APIs)

What to update:
```markdown
## Core
- **New Dependency**: [Package] — [Why we use it]

## Backend
[Update if database, auth, API changes]

## Infrastructure
[Update if hosting, CI/CD changes]
```

#### `docs/WORKFLOW.md`

Update if:
- Development process changed
- New slash commands added
- Workflow phases modified

Usually this stays stable.

#### `docs/decisions/`

Add new ADR if:
- Major architectural decision was made
- Technology choice was made (why X over Y)
- Breaking change was introduced

ADR format:
```markdown
# ADR [Number]: [Title]

**Date**: YYYY-MM-DD  
**Status**: Accepted | Deprecated | Superseded

## Context
[What problem are we solving?]

## Decision
[What did we decide to do?]

## Rationale
[Why this choice over alternatives?]

## Consequences
**Positive**:
- [Benefit 1]

**Negative**:
- [Tradeoff 1]

## Alternatives Considered
- **Option 1**: [Why not chosen]
- **Option 2**: [Why not chosen]
```

#### `plans/[active-plan].md`

Update:
- Mark plan status as `Status: Completed`
- Ensure all checkboxes are `[x] 🟩`
- Add completion date
- Note any deviations from original plan

---

## Documentation Style

**Concise** — Sacrifice grammar for brevity

❌ Bad:
> "The authentication system has been carefully designed to provide secure access control by implementing JSON Web Tokens with refresh token rotation, which enhances security while maintaining a good user experience."

✅ Good:
> "Auth: JWT with refresh token rotation. Secure + good UX."

**Practical** — Examples over theory

❌ Bad:
> "The system uses a repository pattern for data access."

✅ Good:
> "Data access via repository pattern. See `src/repositories/UserRepo.ts` for example."

**Accurate** — Code verified, not assumed

❌ Bad:
> "The app uses Redux for state management." (without checking)

✅ Good:
> [Read package.json, see Zustand installed]  
> "State: Zustand (lightweight alternative to Redux)"

**Current** — Matches actual implementation

❌ Bad:
> "Database: MongoDB" (but code uses Supabase now)

✅ Good:
> [Read actual database config]  
> "Database: Supabase (Postgres)"

---

## Common Documentation Mistakes

### ❌ Mistake 1: Outdated Info

**Problem**: Docs say one thing, code does another

**Example**:
```markdown
# WRONG (docs)
Authentication: Firebase Auth

# ACTUAL (code)
import { supabase } from './supabase'
```

**Fix**: Read the code first, then update docs

### ❌ Mistake 2: Over-Documenting

**Problem**: Documenting every single file/function

**Example**:
```markdown
# Too detailed
- `src/utils/formatDate.ts` — Formats dates
- `src/utils/validateEmail.ts` — Validates emails
- `src/utils/capitalize.ts` — Capitalizes strings
[... 50 more utils ...]
```

**Fix**: Document high-level architecture, not every utility

✅ Better:
```markdown
- `src/utils/` — Helper functions (formatting, validation, etc.)
```

### ❌ Mistake 3: No Examples

**Problem**: Describes what, not how

**Example**:
```markdown
# WRONG
The app has a modular architecture with separation of concerns.
```

**Fix**: Show the structure

✅ Better:
```markdown
## Architecture

```
src/
├── components/   ← React components (UI only)
├── services/     ← Business logic (API calls, processing)
├── hooks/        ← Custom React hooks
└── utils/        ← Pure functions (formatting, validation)
```

Each layer has clear responsibility. Components call hooks. Hooks call services.
```

---

## When to Skip Documentation

**Do NOT update docs if**:
- Only tiny code changes (typo fixes, style tweaks)
- Internal refactoring (no API changes)
- Temporary/experimental changes

**DO update docs if**:
- Public API changed
- Architecture changed
- New features added
- Dependencies changed
- Critical decisions made

---

## After Documentation

Report what you updated:

```markdown
## Documentation Updated

### Files Modified
- `docs/ARCHITECTURE.md` — Added new QuizQuestion type to data model
- `docs/TECH-STACK.md` — Added react-beautiful-dnd dependency
- `docs/decisions/002-drag-drop-library.md` — ADR for choosing react-beautiful-dnd

### Active Plan
- `plans/fill-in-blank-questions-plan.md` — Marked as Status: Completed

---

### Next Steps

Documentation is now in sync with code.

**Recommended**: 
1. Run `/learn` if any complex concepts need understanding
2. Create next issue with `/create-issue` if more work planned
```

---

## Edge Cases

**Q: What if I'm uncertain about documenting something?**  
A: Ask the user. Don't guess.

**Q: What if documentation is massively out of date?**  
A: Flag it, but only fix what's relevant to current changes. Full doc rewrite is a separate task.

**Q: What if there are no docs yet?**  
A: Start with `docs/ARCHITECTURE.md` using the template. Keep it short.

---

**Remember**: Documentation is for future AI agents and humans. Make it accurate, concise, and helpful. When in doubt, read the code first.
