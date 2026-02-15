# Create Plan

Based on our exploration exchange, produce a markdown implementation plan.

---

## Requirements

- **Clear, minimal, concise steps** — no complexity beyond what we discussed
- **Progress tracking** — emoji status for each step
  - 🟩 Done
  - 🟨 In Progress
  - 🟥 To Do
- **Dynamic progress percentage** — calculate as steps complete
- **Modular steps** — each step should be independently testable
- **Integrate with existing code** — follow current patterns

---

## Output File

Save to: `plans/[feature-name]-plan.md`

Use slug format: `fill-in-blank-questions-plan.md`, `dark-mode-toggle-plan.md`

---

## Plan Template

```markdown
# [Feature Name] Implementation Plan

**Overall Progress:** `0%`  
**Created:** [YYYY-MM-DD]  
**Status:** Active | Completed | Paused

---

## TL;DR

[2-3 sentences: What we're building and why]

---

## Critical Decisions

Key architectural/implementation choices made during exploration:

- **Decision 1**: [Choice made] — [Rationale]
- **Decision 2**: [Choice made] — [Rationale]
- **Decision 3**: [Choice made] — [Rationale]

---

## Tasks

### Phase 1: [Phase Name - e.g., "Data Model"]

- [ ] 🟥 **Task 1.1: [Task Name]**
  - [ ] 🟥 Subtask A — `path/to/file.ts` — [what to change]
  - [ ] 🟥 Subtask B — `path/to/file.ts` — [what to change]

- [ ] 🟥 **Task 1.2: [Task Name]**
  - [ ] 🟥 Subtask A — `path/to/file.ts` — [what to change]

### Phase 2: [Phase Name - e.g., "Business Logic"]

- [ ] 🟥 **Task 2.1: [Task Name]**
  - [ ] 🟥 Subtask A — `path/to/file.ts` — [what to change]
  - [ ] 🟥 Subtask B — `path/to/file.ts` — [what to change]

### Phase 3: [Phase Name - e.g., "UI Components"]

- [ ] 🟥 **Task 3.1: [Task Name]**
  - [ ] 🟥 Subtask A — `path/to/file.tsx` — [what to change]

### Phase 4: [Phase Name - e.g., "Testing & Polish"]

- [ ] 🟥 **Task 4.1: Manual Testing**
  - [ ] 🟥 Test scenario 1
  - [ ] 🟥 Test scenario 2
  - [ ] 🟥 Test scenario 3

- [ ] 🟥 **Task 4.2: Code Review**
  - [ ] 🟥 Run `/review` (self-review)
  - [ ] 🟥 Run `/peer-review` (cross-model validation)

- [ ] 🟥 **Task 4.3: Documentation**
  - [ ] 🟥 Run `/document` to update docs
  - [ ] 🟥 Mark this plan as Complete

---

## Risks / Notes

- **Risk 1**: [What could go wrong] — [Mitigation strategy]
- **Risk 2**: [What could go wrong] — [Mitigation strategy]

---

## Dependencies

- [Dependency 1]: [Why it matters]
- [Dependency 2]: [Why it matters]

---

## Testing Strategy

**Manual testing**:
1. [Test scenario 1]
2. [Test scenario 2]
3. [Test scenario 3]

**Automated testing** (if applicable):
- [Test file]: `tests/[feature].test.ts` — [What to test]

---

## Rollback Plan

If this goes wrong:
1. [How to undo changes]
2. [What to revert]
3. [How to notify users if live]

---

## Estimated Effort

- **Phase 1**: [time estimate]
- **Phase 2**: [time estimate]
- **Phase 3**: [time estimate]
- **Phase 4**: [time estimate]

**Total**: [total estimate]

---

## Next Steps

1. Get user approval on this plan
2. Run `/execute` to implement
3. Update this file as steps complete (change 🟥 → 🟨 → 🟩)
4. After execution: `/review` → `/peer-review` → `/document`
```

---

## Rules

- **Still NOT time to build** — just write the plan document
- **No extra complexity** beyond what we discussed in exploration
- **Each step should be modular** — independently completable and testable
- **Link to specific files** — make it actionable
- **Include rollback** — always have an undo strategy

---

## Plan Quality Checklist

Before finalizing the plan, verify:

✅ Every step links to specific files  
✅ No vague steps like "implement feature" (break it down)  
✅ Critical decisions are documented  
✅ Risks are identified with mitigations  
✅ Testing strategy is clear  
✅ Rollback plan exists  
✅ Progress tracking is in place  

---

## After Creating the Plan

**Do NOT execute yet.** Present the plan to the user:

> "✅ Implementation plan created: `plans/[feature-name]-plan.md`
> 
> **Summary**:
> - [X] phases
> - [Y] total tasks
> - Est. [Z] hours
> 
> **Critical decisions**:
> - [Decision 1]
> - [Decision 2]
> 
> **Risks**:
> - [Risk 1]
> 
> Ready to proceed? If yes, run `/execute` to implement."

Wait for user approval before executing.

---

**Remember**: A good plan prevents mistakes. The plan is the contract for what gets built. Get it right before coding.
