# Development Workflow

How we build features in this project.

---

## Overview

We follow an **8-phase development process** enforced by slash commands.

Each phase has a specific purpose and output. You can't skip phases.

---

## The 8 Phases

### 1. Capture (`/create-issue`)

**When**: Mid-development, you think of a bug or new feature

**Goal**: Capture it quickly without breaking flow

**Process**:
1. Run `/create-issue`
2. Briefly describe the idea/bug
3. AI asks 2-3 clarifying questions
4. Issue saved to `docs/backlog/YYYY-MM-DD-[title].md`

**Output**: Markdown issue file in backlog

**Time**: ~2 minutes

**Example**:
> "I need to add dark mode toggle to settings"  
> → AI creates `docs/backlog/2026-02-15-dark-mode-toggle.md`

---

### 2. Explore (`/explore`)

**When**: Ready to start working on an issue

**Goal**: Deeply understand the problem before writing any code

**Process**:
1. Run `/explore` (optionally with issue file)
2. AI reads codebase and analyzes affected areas
3. AI asks ALL clarifying questions
4. Back-and-forth until zero ambiguity

**Output**: Complete understanding of:
- Current code state
- Files to modify
- Dependencies
- Edge cases
- Implementation approach

**Time**: 10-30 minutes (depending on complexity)

**Critical**: NO CODE WRITTEN during exploration

---

### 3. Plan (`/create-plan`)

**When**: After exploration is complete

**Goal**: Create a concrete, step-by-step implementation plan

**Process**:
1. Run `/create-plan`
2. AI generates markdown plan with:
   - Progress tracking (emoji status)
   - Phases and tasks
   - Critical decisions
   - Risks and mitigations

**Output**: `plans/[feature-name]-plan.md`

**Time**: 5-15 minutes

**Approval**: User reviews plan before execution

---

### 4. Execute (`/execute`)

**When**: After plan is approved

**Goal**: Implement the plan step-by-step

**Process**:
1. Run `/execute`
2. AI reads plan and implements each task in order
3. AI updates plan file as steps complete (🟥 → 🟨 → 🟩)
4. User can pause/resume at any point

**Output**: Code changes according to plan

**Time**: 15 minutes to several hours (depends on feature size)

**Model choice**:
- **Claude Code**: Complex logic, architecture
- **Cursor Composer**: Fast, simple tasks
- **Codex**: Gnarly bugs

---

### 5. Review (`/review`)

**When**: After execution completes

**Goal**: Self-review for bugs and quality issues

**Process**:
1. Run `/review`
2. AI checks code against quality checklist:
   - Logging
   - Error handling
   - TypeScript
   - Production readiness
   - Performance
   - Security
   - Architecture

**Output**: List of issues by severity (CRITICAL, HIGH, MEDIUM, LOW)

**Time**: 5-10 minutes

**Next**: Fix critical/high issues before proceeding

---

### 6. Peer Review (`/peer-review`)

**When**: After self-review

**Goal**: Cross-model validation (different AI catches different bugs)

**Process**:
1. User switches to different model (e.g., Codex)
2. User runs review in that model: "Review all changes in this branch"
3. User copies findings
4. User switches back to primary model (Claude Code)
5. Run `/peer-review` and paste findings
6. AI validates each finding (has more context than peer)
7. AI produces list of confirmed issues

**Output**: Validated fix list (rejects false positives)

**Time**: 10-20 minutes

**Critical**: "Less context" framing prevents blind acceptance

---

### 7. Document (`/document`)

**When**: After all fixes are done

**Goal**: Keep documentation in sync with code

**Process**:
1. Run `/document`
2. AI reads actual code (not docs)
3. AI updates relevant files:
   - `docs/ARCHITECTURE.md`
   - `docs/TECH-STACK.md`
   - `docs/decisions/` (if new ADR needed)
   - Plan file (mark as complete)

**Output**: Updated documentation

**Time**: 5-10 minutes

---

### 8. Learn (`/learn`)

**When**: Anytime something is confusing

**Goal**: Understand complex concepts, not just execute

**Process**:
1. Run `/learn [topic]`
2. AI explains in 3 levels:
   - Level 1: Core concept (what, why, when)
   - Level 2: How it works (mechanics, tradeoffs)
   - Level 3: Deep dive (production implications)
3. Uses 80/20 rule (practical over academic)

**Output**: Deep understanding

**Time**: 5-15 minutes

**Use**: During exploration, debugging, or after completing feature

---

## Visual Workflow

```
Idea/Bug
   ↓
/create-issue → docs/backlog/[issue].md
   ↓
/explore → Understanding + Questions
   ↓
/create-plan → plans/[plan].md
   ↓
   [User approves plan]
   ↓
/execute → Code changes
   ↓
/review → Self-review findings
   ↓
   [Fix critical/high issues]
   ↓
/peer-review → Cross-model validation
   ↓
   [Fix confirmed issues]
   ↓
/document → Updated docs
   ↓
   ✅ Feature complete
   
   [Optional: /learn anytime]
```

---

## Multi-Model Strategy

Three AI tools work on this project simultaneously:

| Tool | When to Use | Strength |
|------|-------------|----------|
| **Claude Code** | Planning, exploration, main dev | Communicative, challenges assumptions |
| **Cursor Composer** | Fast, simple tasks | Blazing speed |
| **Codex (GPT)** | Debugging, peer review | Deep problem-solving |

**Switching**: 
- All tools read same project files (`CLAUDE.md`, docs/, plans/)
- No copy/paste needed (unlike separate ChatGPT window)
- Context preserved across tools

---

## Postmortem Process

**When AI makes a mistake** (wrong implementation, missed requirement, etc.):

1. **Reflect**: Ask AI "What in your prompt or context caused this mistake?"
2. **Analyze root cause**:
   - Ambiguous system prompt?
   - Missing documentation?
   - Misunderstood architecture?
3. **Update the right file**:
   - `CLAUDE.md` if prompt issue
   - `docs/` if context issue
   - `.claude/commands/` if slash command issue
4. **Goal**: Prevent this mistake from recurring

**Log**: Keep a running list in `docs/postmortems.md` (optional)

---

## Decision Points

**Q: Should I skip exploration and go straight to coding?**  
A: NO. Exploration prevents mistakes. Always `/explore` first.

**Q: Can I execute without a plan?**  
A: NO for complex features. YES for tiny fixes (typos, style).

**Q: Can I skip peer review?**  
A: Not recommended. Peer review catches blind spots.

**Q: When should I use `/learn` vs `/explore`?**  
A: `/explore` = understand WHAT to build. `/learn` = understand HOW it works.

---

## Workflow Variations

### For Small Fixes

```
/create-issue (optional)
  ↓
Quick fix in code
  ↓
/review
  ↓
Ship
```

### For New Projects

```
Set up CLAUDE.md with tech stack
  ↓
Create docs/ARCHITECTURE.md
  ↓
/create-issue for first feature
  ↓
Normal workflow
```

### For Research/Exploration

```
/learn [topic]
  ↓
/explore implementation approach
  ↓
/create-issue with findings
  ↓
Normal workflow
```

---

## File Structure Awareness

Before starting work:

✅ Check `plans/` for active work (don't conflict)  
✅ Check `docs/backlog/` for related issues  
✅ Read `docs/ARCHITECTURE.md` for system context  
✅ Read `docs/decisions/` for past decisions  

---

## Quality Gates

**Before shipping**:

✅ All CRITICAL issues fixed (from `/review`)  
✅ All HIGH issues fixed (from `/review`)  
✅ Peer review completed (via `/peer-review`)  
✅ Documentation updated (via `/document`)  
✅ Manual testing done  
✅ No console.log or debug code  
✅ No TODO comments (create issues instead)  

---

## Tips for Success

1. **Don't rush exploration** — time here saves debugging time later
2. **Get plan approval** — surprises are bad
3. **Update plan as you go** — keeps progress visible
4. **Run peer review every time** — different models catch different bugs
5. **Use `/learn` liberally** — understanding compounds
6. **Run postmortems** — improve the system continuously

---

**Remember**: This workflow exists to catch mistakes early. Follow it, even when it feels slow. Speed comes from not having to redo work.
