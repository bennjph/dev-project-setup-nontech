# Execute Plan

Implement the plan precisely as written.

---

## Process

### 1. Read the Plan

Locate the plan file in `plans/[feature-name]-plan.md`.

Read it thoroughly:
- Understand the overall goal (TL;DR)
- Review critical decisions
- Understand each phase and task
- Note any risks or dependencies

### 2. Implement in Order

Work through tasks sequentially:

1. **Start a task** → Update status: `- [ ] 🟥` → `- [ ] 🟨`
2. **Complete subtasks** within that task
3. **Finish task** → Update status: `- [ ] 🟨` → `- [x] 🟩`
4. **Move to next task**

### 3. Update the Plan as You Go

**IMPORTANT**: After completing each major task, update the plan file:

- Change emoji from 🟥 (To Do) → 🟨 (In Progress) → 🟩 (Done)
- Check the checkbox when task is complete: `- [x] 🟩`
- Update overall progress percentage at top

Example:
```markdown
**Overall Progress:** `25%`   <- Update this

- [x] 🟩 **Task 1.1: Extend QuizQuestion type**  <- Completed
  - [x] 🟩 Add fillInBlank field
  - [x] 🟩 Add validation

- [ ] 🟨 **Task 1.2: Update database schema**    <- In Progress
  - [x] 🟩 Create migration                       <- Done
  - [ ] 🟨 Test migration locally                 <- Working on this
```

### 4. Write Clean Code

Follow these standards:

**Code Quality**:
- Minimal, modular, elegant code
- Follow existing project patterns
- Clear variable and function names
- Comments for complex logic only

**TypeScript** (if applicable):
- Proper type definitions
- No `any` types
- Interfaces for objects

**Error Handling**:
- Try-catch for async operations
- Meaningful error messages
- Handle edge cases identified in plan

**Performance**:
- No unnecessary operations
- Optimize expensive calculations
- Avoid memory leaks

### 5. Test as You Go

For each major task completed:

1. **Manual test** the changes
2. **Check edge cases** from the plan
3. **Verify** no regressions in existing features

If something breaks: STOP, document the issue, ask for help.

### 6. Commit Strategy (if using git)

Make logical commits:
- One commit per major task (not per line changed)
- Clear commit messages referencing the plan
- Example: `feat: Add fill-in-blank question type (Task 1.1)`

---

## Rules

- **Adhere strictly to the plan** — no scope creep
- **If something is unclear**: STOP and ask before implementing
- **If you discover a blocker**: STOP, update plan with status, explain
- **Update plan file** after each task completion
- **No TODO comments** — if you can't finish, create an issue
- **No console.log** — use proper logging
- **No hardcoded values** — use config/env vars

---

## Blockers / Unexpected Issues

If you encounter a problem during execution:

1. **Stop implementation**
2. **Document the blocker** in the plan:
   ```markdown
   ## Blockers

   - **[Date]**: [Description of blocker]
     - Attempted: [What you tried]
     - Needs: [What's needed to unblock]
   ```
3. **Ask the user** for guidance
4. **Update plan status**: Mark task as 🟨 (paused) or add note

**Do NOT**:
- Guess at solutions
- Implement workarounds without approval
- Silently skip tasks

---

## Example Execution Flow

```markdown
User runs: /execute

You:
> "Reading plan: `plans/fill-in-blank-questions-plan.md`
> 
> **Plan Summary**:
> - 4 phases
> - 12 tasks total
> - Current progress: 0%
> 
> Starting execution..."

[You implement Task 1.1]

> "✅ Task 1.1 complete: Extended QuizQuestion type
>    - Added fillInBlank field with proper typing
>    - Updated Zod validation schema
>    - Updated plan: 8% progress
> 
> Moving to Task 1.2: Update database schema..."

[You implement Task 1.2]

> "✅ Task 1.2 complete: Database schema updated
>    - Created migration file
>    - Tested migration locally
>    - Updated plan: 17% progress
> 
> Phase 1 (Data Model) complete ✅
> 
> Moving to Phase 2: Business Logic..."

[Continue through all tasks]

> "✅ All phases complete!
>    - Updated plan: 100% progress
>    - Status: Ready for review
> 
> **Next steps**:
> 1. Run `/review` for self-review
> 2. Manual QA testing
> 3. Run `/peer-review` for cross-model validation"
```

---

## After Execution

When all tasks are complete:

1. **Update plan status** to `Status: Ready for Review`
2. **Verify** all checkboxes are `[x] 🟩`
3. **Verify** progress is `100%`
4. **Run manual tests** from plan's Testing Strategy
5. **Report completion** to user

Then prompt user to run `/review`.

---

## Mid-Execution Pause

If user needs to pause:

1. **Update plan** with current status (🟨 emojis where paused)
2. **Save any uncommitted work**
3. **Document** what's left in plan
4. **Update** progress percentage

To resume later: Re-run `/execute`, and you'll pick up where you left off.

---

## Quality Reminders

Before marking any task as 🟩 (Done):

✅ Code works (you tested it)  
✅ No errors or warnings  
✅ Follows existing patterns  
✅ Edge cases handled  
✅ No console.log or debug code  
✅ Proper error handling  
✅ Comments only where needed  

---

**Remember**: The plan is your contract. Stick to it. If you need to deviate, STOP and discuss with the user first. Surprises are bad.
