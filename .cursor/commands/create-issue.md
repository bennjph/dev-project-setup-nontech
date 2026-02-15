# Create Issue

User is mid-development and thought of a bug, feature, or improvement.  
**Capture it fast so they can keep working.**

---

## Your Goal

Create a complete issue document with:
- Clear, concise title
- TL;DR (1-2 sentences)
- Current state vs expected outcome
- Relevant files (from codebase search)
- Risk/notes if applicable
- Type (bug/feature/improvement) and priority

---

## Process

1. **Ask 2-3 brief clarifying questions** (respect mid-flow time)
   - What's the core issue/feature?
   - Current behavior vs desired behavior?
   - Priority if not obvious?

2. **Search codebase for relevant files** (max 3 files)
   - Find where this would be implemented
   - Note dependencies

3. **Create issue file**: `docs/backlog/YYYY-MM-DD-[title-slug].md`

---

## Issue File Template

```markdown
# [Clear, Concise Title]

**Type**: bug | feature | improvement  
**Priority**: critical | high | medium | low  
**Created**: [YYYY-MM-DD]

## TL;DR
[1-2 sentences describing the issue/feature]

## Current State
[What exists now or what's broken]

## Expected Outcome
[What should happen after this is done]

## Relevant Files
- `path/to/file.ts` — [why this file is relevant]
- `path/to/another.ts` — [why relevant]

## Notes / Risks
- [Any technical risks, dependencies, or important context]
- [Leave this section empty if none]

## Next Steps
1. Run `/explore` to analyze this issue thoroughly
2. Run `/create-plan` to generate implementation plan
```

---

## Behavior Rules

- **Be conversational** — ask only what's needed, not a checklist
- **Be fast** — max 2 minutes total interaction
- **Default values**: priority=medium, type inferred from description
- **Max 3 relevant files** — most impactful ones only
- **Use bullets** — prefer lists over paragraphs

---

## Example Interaction

**User**: "I need to add dark mode toggle to settings"

**You**: "Quick questions:
1. Where should the toggle appear? (Settings page, nav bar, both?)
2. Should it persist across sessions?
3. Priority? (I'm guessing medium)"

**User**: "Settings page, yes persist, medium priority"

**You**: 
"✅ Created issue: `docs/backlog/2026-02-15-dark-mode-toggle-settings.md`

**Next steps**:
- Run `/explore` when ready to start working on this
- I found 2 relevant files: `src/components/Settings.tsx` and `src/contexts/ThemeContext.tsx`"

---

## Edge Cases

- **User provides full description**: Don't ask unnecessary questions
- **Unclear scope**: Ask clarifying questions
- **Duplicate issue**: Search `docs/backlog/` first, warn if similar exists

---

**Remember**: You're capturing this MID-FLOW. Speed and clarity matter. Don't over-engineer the issue — just get it documented so work can continue.
