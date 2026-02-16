# First Principles Analysis: Agentic AI Dev Team Setup
**Source**: https://github.com/bennjph/agentic-ai-dev-team-setup  
**Analysis Date**: 2026-02-16  
**Context**: Elite product development workflow for AI-assisted development

---

## 🎯 **The Core First Principles**

### 1. **Process Over Tools** (Tool-Agnostic Philosophy)
- **Principle**: Value lies in the *discipline*, not the tooling
- **Why it matters**: You can switch AI tools (OpenCode → Cursor → Claude) but the workflow remains constant
- **Application**: Focus on building repeatable processes, not becoming dependent on specific vendors
- **Evidence**: Synthesized from Google SRE, DORA, Martin Fowler, Linear Method

### 2. **Make the Implicit Explicit** (The Unifying Meta-Principle)
> *"The biggest cost in software isn't writing code — it's the information that lives in people's heads and disappears when they context-switch, leave, or forget."*

- **Principle**: Convert all implicit knowledge into explicit, version-controlled artifacts
- **Why it matters**: Prevents knowledge loss, enables async collaboration, forces clarity of thought
- **Application**: 
  - Implicit understanding → Explicit exploration doc
  - Implicit plan → Explicit plan file with tasks
  - Implicit quality bar → Explicit 5-dimension review rubric
  - Implicit lessons → Explicit knowledge vault
  - Implicit handoff → Explicit SBAR document
  - Implicit process → Explicit tier config
- **Artifacts Created**:
  - `plans/` — Exploration and implementation plans
  - `decisions/` — Architecture Decision Records (ADRs)
  - `knowledge/` — Searchable solution vault
  - `retros/` — Postmortems and retrospectives
  - `rfcs/` — Team decision proposals
  - `handoffs/` — Context transfer between teammates

### 3. **Strategy-Execution Separation** (Think Before You Code)
- **Principle**: Always explore and plan *before* building (NO CODE during exploration)
- **Why it matters**: Prevents coding yourself into a corner; reduces rework
- **Application**: `/explore` (understand) → `/plan` (break down) → `/build` (implement)
- **Key Rule**: Writing code during `/explore` is **forbidden** — exploration is about understanding, not implementation

### 4. **"Less Context" Review** (Objective Evaluation Through Constraint)
- **Principle**: Reviewers see only the code diff + one-sentence intent, NOT the creation conversation
- **Why it matters**: Forces evaluation of code on its own merits, prevents anchoring bias from builder's reasoning
- **Application**: 
  - Builder works with full context
  - Reviewer receives: code changes + brief intent statement
  - Reviewer must judge: "Does this code clearly do what the intent says?"
- **Result**: Code must be self-documenting and clear without explanation

### 5. **Cognitive Mode Specialization** (Agents by Thinking, Not Tasks)
- **Principle**: Organize agents by *how they think*, not *what they build*
- **Why it matters**: Prevents muddled "do everything at once" mode; mirrors how real teams work
- **The 6 Cognitive Modes**:
  1. **Analytical** (Sherlock) — Investigate, explore, research
  2. **Strategic** (Jared)* — Plan, decide, prioritize
  3. **Generative** (Stallion)* — Build, implement, create
  4. **Evaluative** (Judge) — Review, critique, validate
  5. **Communicative** (Scriptor) — Document, explain, transfer
  6. **Orchestrative** (Moss)* — Route, coordinate, manage
- **Application**: A single prompt trying to plan, build, and review simultaneously will do all three poorly

*Agent names reference characters from HBO's *Silicon Valley* and Channel 4's *The IT Crowd*

### 6. **Progressive Complexity** (Tiered Adoption)
- **Principle**: Start simple (5 practices), scale up as you grow (10 → 15 practices)
- **Why it matters**: Avoids overwhelming teams with process; allows organic adoption
- **Application**: 
  - **Tier 1 (Solo)**: 5 essential practices
    1. Trunk-based development
    2. Self-testing code (TDD)
    3. Small batch delivery (< 200 LOC)
    4. Strategy-execution split
    5. Cross-model review
  - **Tier 2 (Team)**: Add coordination (10 practices)
    6. Feature flags
    7. Postmortems (5 Whys)
    8. Observability
    9. Compound learning
    10. Visual progress tracking
  - **Tier 3 (Enterprise)**: Full rigor (15 practices)
    11. Architecture Decision Records
    12. Multi-model validation
    13. Tiered teaching
    14. Workflow phasing
    15. Architecture review

### 7. **Cross-Model Validation** (Different Perspectives Catch Different Bugs)
- **Principle**: Use different AI models to review than to build (different providers preferred)
- **Why it matters**: Same model = same blind spots; diversity improves quality
- **Application**: Builder uses GPT-5 → Reviewer uses Claude Sonnet 4.5
- **Research**: Multi-Model Validation Research (arxiv.org/abs/2405.00964)

---

## 🔧 **The Core Workflow Principles**

### 8. **Small Batch Delivery** (Ship in Increments)
- **Principle**: Keep changes < 200 lines of code per commit
- **Why it matters**: Lower risk, faster feedback, easier to review
- **Application**: Break features into vertical slices that are independently shippable
- **Example**:
  - ❌ **Bad**: Implement entire auth system (800 LOC, 1 commit)
  - ✅ **Good**: 
    - Commit 1: Login form UI (50 LOC)
    - Commit 2: Login API endpoint (80 LOC)
    - Commit 3: Connect form to API (40 LOC)
    - Commit 4: Add error handling (30 LOC)

### 9. **Test-Driven Development** (Tests First, Code Second)
- **Principle**: Write failing test → Make it pass → Refactor (RED → GREEN → CLEAN)
- **Why it matters**: Prevents regressions, enables fearless refactoring, acts as living documentation
- **Application**: Every feature starts with a test
- **Source**: Test-Driven Development (Kent Beck), Martin Fowler

### 10. **Verification Gates as Quality Ratchet** (Structural Quality Enforcement)
- **Principle**: Quality is enforced structurally through mandatory review checkpoints, not hoped for
- **Why it matters**: Makes quality a system property, not an individual virtue
- **Application**: After any agent produces output, it routes through Reviewer for SHIP/REVISE/BLOCK verdict
- **Result**: The default path produces good output; good practices become the path of least resistance

### 11. **Blameless System Improvement** (Focus on Process Gaps, Not People)
- **Principle**: Retrospectives use 5 Whys to drill down to system/process gaps, never individual mistakes
- **Why it matters**: Optimizes for future prevention over past punishment; creates psychological safety
- **Application**: 
  - "Why did this bug ship?" 
  - → "Tests didn't cover this edge case" 
  - → "Our test plan template doesn't prompt for boundary conditions" 
  - → **Update the template**
- **Source**: Google SRE's blameless postmortem culture
- **Result**: Team focuses on identifying and fixing system gaps, not assigning blame

### 12. **Compound Learning** (Build Institutional Knowledge)
- **Principle**: Extract learnings from retrospectives into reusable knowledge docs
- **Why it matters**: Don't solve the same problem twice; faster onboarding
- **Application**: `retros/` → `knowledge/solutions/` (searchable vault)
- **Process**:
  1. Solve hard problem
  2. Run `/retro` (identify system gap)
  3. Extract to `knowledge/[topic].md`
  4. Next time: Search knowledge first
- **Source**: NASA Knowledge Management practices
- **Key Insight**: Solving the same problem twice is a process failure, not a people failure

---

## 🤖 **The AI-Specific Principles**

### 13. **Progressive Autonomy** (Earn Trust Before Granting Freedom)
- **Principle**: Always start with high control, low agency (V1), then gradually increase based on demonstrated reliability
- **Why it matters**: Prevents debugging 100 failure modes simultaneously; trust is built incrementally through evidence
- **Application**: 
  - **V1 (Low Agency)**: Human approves everything, AI suggests
  - **V2 (Medium Agency)**: AI suggests, human can override
  - **V3 (High Agency)**: AI acts autonomously, human monitors
- **Critical Rule**: Never skip V1 and go straight to V2/V3
- **Note**: Autonomy is granted based on evidence, not assumed. This applies to AI agents, team members, and systems alike.

### 14. **Continuous Calibration** (Observe → Fix → Verify)
- **Principle**: Deploy at low scale (10%), observe behavior for 1-2 weeks, tune before scaling
- **Why it matters**: Non-deterministic systems need production data to improve
- **Application**: `/calibrate` command between each version increase
- **Process**:
  - **Week 1**: Deploy & Observe (10-25% users)
  - **Week 2**: Analyze & Fix (recurring patterns)
  - **Decision**: Ready for next version?
- **Key Metrics**:
  - Explicit signals: User ratings, feedback, bug reports
  - Implicit signals: Regeneration rate, edit distance, feature toggle-offs

### 15. **Measurement as a First Principle** (You Can't Improve What You Don't Measure)
- **Principle**: Define success metrics upfront; track them continuously; adjust process when metrics decline
- **Why it matters**: Makes quality and progress objective, not subjective; enables data-driven improvement
- **Application**: 
  - Time to ship feature: < 1 week
  - Test coverage: > 80%
  - Repeat incidents: < 10%
  - Code review turnaround: < 24 hours
  - Time to onboard new dev: < 1 day (with docs)
- **Process**: Track monthly, adjust practices if metrics decline
- **Example**: If "repeat incidents" rises above 10%, investigate retro process and knowledge capture

---

## 📊 **The Evidence-Based Foundation**

All practices are grounded in research from:
- **Google SRE** (Site Reliability Engineering) — Reliability patterns
- **DORA** (DevOps Research & Assessment) — Research-backed metrics
- **Martin Fowler** (Continuous Integration, Feature Flags) — Software architecture
- **Linear Method** (Small batch delivery) — Product development
- **Elite dev workflows** (Zevi, Replit, Vercel) — "Less context" peer review

**Key insight**: These aren't opinions—they're proven patterns from elite teams.

---

## 🎬 **The 7 Workflow Commands**

| Command | Purpose | Artifact Created | Tier |
|---------|---------|------------------|------|
| `/explore` | Spike without code (NO CODE exploration) | `backlog/explorations/EXP-NNN.md` | All |
| `/plan` | Turn issue into executable plan | `plans/PLAN-NNN.md` | All |
| `/build` | Implement with TDD (small batches) | Code + tests | All |
| `/review` | Cross-model code review (SHIP/REVISE/BLOCK) | `decisions/code-review-YYYY-MM-DD-NNN.md` | All |
| `/retro` | Postmortem learning (5 Whys) | `retros/RETRO-YYYY-MM-DD.md` | All |
| `/rfc` | Architecture decision record (ADR) | `rfcs/RFC-NNN-title.md` | Team+ |
| `/handoff` | Context transfer (SBAR format) | `handoffs/HANDOFF-YYYY-MM-DD-feature.md` | Team+ |

### Standard Workflow
```
explore → plan → build → review → retro
```

### AI Features Workflow
```
explore → plan → build → calibrate → review → retro
```

---

## 💡 **Key Innovations in Practice**

### 1. NO CODE Exploration
**Writing code during `/explore` is forbidden.** Exploration is about understanding, not implementation.

**Why?** Code commits you to a solution before you understand the problem.

---

### 2. "Less Context" Review + Cross-Model Validation
**Builder uses Model A with full context → Reviewer uses Model B with minimal context** (code diff + one-sentence intent only).

**Why?** 
- Different models catch different bugs (ensemble thinking)
- Limited context forces objective evaluation
- Code must be self-documenting

**Example**:
- Builder (GPT-5.3) works with full conversation history
- Reviewer (Claude Sonnet 4.5) sees only: "Add user authentication" + code diff
- Reviewer must judge: "Does this code clearly implement auth?"

---

### 3. Cognitive Mode Specialization
Agents aren't organized by domain (frontend/backend) but by **thinking mode**:
- Analytical → Explore
- Strategic → Plan  
- Generative → Build
- Evaluative → Review
- Communicative → Document
- Orchestrative → Coordinate

**Why?** Mirrors how real teams work; prevents muddled "do everything at once" mode.

---

### 4. Structural Quality Enforcement
Quality isn't hoped for — it's **enforced by the system**:
- Mandatory review gates (SHIP/REVISE/BLOCK)
- NO CODE rule during exploration
- TDD requirement (test before code)
- Artifact requirement (if not written, not done)

**Result**: Good practices become automatic, not optional.

---

### 5. Blameless System Improvement
Retros focus on **system gaps**, not individual mistakes:
- 5 Whys always leads to process improvement
- "Why did bug ship?" → "Template didn't prompt for edge cases" → Fix template
- Creates psychological safety + continuous improvement

---

### 6. Tier-Based Scaling
**Solo** (5 practices, 5 commands) → **Team** (10 practices, 7 commands) → **Enterprise** (15 practices, strict gates)

Start simple. Add rigor as you scale.

---

## 🎯 **Practical Application Patterns**

### Pattern 1: New Feature (Happy Path)
```
/explore "Add user notifications" 
  ↓
Convert to backlog/issues/ISSUE-042.md
  ↓
/plan backlog/issues/ISSUE-042.md
  ↓
/build plans/PLAN-042.md (small batches, TDD)
  ↓
/review plans/PLAN-042.md
  ↓
Ship ✅
  ↓
/retro "Notifications shipped"
```

---

### Pattern 2: Architecture Decision (Team)
```
Problem: Need to choose API framework
  ↓
/rfc "Proposal: FastAPI vs Flask for new microservice"
  ↓
Team reviews rfcs/RFC-013-api-framework.md
  ↓
Decision: FastAPI (update RFC status → accepted)
  ↓
/plan "Implement auth service with FastAPI"
  ↓
[build → review → ship]
```

---

### Pattern 3: Bug Fix with Learning
```
Bug reported: API timeouts in production
  ↓
/explore "Why are API calls timing out?"
  ↓
/plan "Fix: Add circuit breaker pattern"
  ↓
/build plans/PLAN-055-circuit-breaker.md
  ↓
/review plans/PLAN-055.md
  ↓
Deploy fix
  ↓
/retro "Postmortem: API timeout cascade" (5 Whys)
  ↓
Extract learning → knowledge/circuit-breaker-pattern.md
```

---

## 📈 **Measurement as a First Principle**

**How to know if it's working** (track monthly, adjust when metrics decline):

| Metric | Target | What It Measures | If Declining, Check... |
|--------|--------|------------------|------------------------|
| Time to ship feature | < 1 week | Delivery speed | Batch size, planning quality |
| Test coverage | > 80% | Code quality | TDD adherence, review rigor |
| Repeat incidents | < 10% | Learning effectiveness | Retro process, knowledge capture |
| Code review turnaround | < 24 hours | Review efficiency | Review load, cross-model setup |
| Time to onboard new dev | < 1 day | Documentation quality | Artifact completeness, knowledge vault |

**Example**: If "repeat incidents" rises above 10%, investigate:
1. Are retros identifying root causes?
2. Are system gaps being fixed?
3. Is knowledge being captured and searched?
4. Are templates/checklists being updated?

**The principle**: Metrics aren't just tracking — they're feedback loops for process improvement.

---

## 🔑 **The Ultimate Meta-Principle**

> *"Make good practices the path of least resistance."*

**The core insight**: The repo doesn't ask developers to remember 15 rules — it **encodes them into commands, agents, templates, and verification gates** so that following the process *is* the easy thing to do.

**The system does the discipline so individuals don't have to.**

- Quality is enforced structurally (verification gates), not hoped for
- Good practices are automatic (encoded in commands), not optional
- Knowledge is captured systematically (artifacts), not lost
- Process scales with complexity (tiers), not one-size-fits-all

**Result**: Ship faster by making the right thing the easy thing.

---

## 🚀 **Adoption Strategy**

**Don't adopt all 15 practices at once.** Start with Tier 1 (5 practices), master them, then add more.

### Month 1: Tier 1 (Solo)
- Trunk-based dev
- TDD
- Small batches
- Strategy-execution split
- Cross-model review

### Month 2-3: Tier 2 (Team)
- Add feature flags
- Add postmortems
- Add compound learning
- Add visual progress tracking

### Month 4+: Tier 3 (Enterprise)
- Add ADRs
- Add multi-model validation
- Add tiered teaching
- Add workflow phasing
- Add architecture review

**Gradual adoption > big-bang transformation.**

---

## 🔗 **Integration with Git**

All artifacts are tracked in git. Recommended commit prefixes:
- `exploration:` — Explorations
- `plan:` — Plans
- `feat:` — Feature code
- `fix:` — Bug fixes
- `review:` — Code reviews
- `retro:` — Retrospectives
- `rfc:` — Architecture decisions
- `handoff:` — Context transfers

---

## 🎓 **Key Takeaways for AI-Assisted Development**

### The 15 Core Principles (Prioritized)

1. **Make Good Practices the Path of Least Resistance** — Encode discipline into the system
2. **Make the Implicit Explicit** — Convert all knowledge into artifacts
3. **Process > Tools** — Workflows survive tool changes
4. **Think Before You Code** — NO CODE during exploration
5. **"Less Context" Review** — Reviewers see only code + intent, not creation conversation
6. **Cognitive Mode Specialization** — Organize by thinking mode, not task type
7. **Small Batch Delivery** — Ship in < 200 LOC increments
8. **Test-Driven Development** — Tests define reality, not an afterthought
9. **Verification Gates** — Quality enforced structurally
10. **Blameless System Improvement** — Focus on process gaps, not people
11. **Compound Learning** — Capture and index all learnings
12. **Cross-Model Validation** — Different models catch different bugs
13. **Progressive Autonomy** — Earn trust through evidence
14. **Continuous Calibration** — Observe before scaling
15. **Measurement as Principle** — Track metrics, adjust when they decline

### Quick Decision Framework

**When starting a feature:**
- ✅ Run `/explore` first (NO CODE)
- ✅ Create explicit plan with tasks
- ✅ Write test before implementation
- ✅ Ship in small batches
- ✅ Use different model for review
- ✅ Capture learnings in retro

**When reviewing code:**
- ✅ See only code diff + brief intent
- ✅ Judge: "Does code clearly do what intent says?"
- ✅ Give explicit verdict: SHIP/REVISE/BLOCK

**When something goes wrong:**
- ✅ Run 5 Whys to find system gap
- ✅ Update process/template/checklist
- ✅ Extract learning to knowledge base
- ❌ Don't blame individuals

---

## 📚 **References**

- [Google SRE Book](https://sre.google/sre-book/)
- [Accelerate (DORA)](https://www.oreilly.com/library/view/accelerate/9781457191435/)
- [Martin Fowler's Bliki](https://martinfowler.com/bliki/)
- [Linear Method](https://linear.app/method)
- [Zevi's Workflow](https://x.com/zevi/status/1871649436998160865)
- [Multi-Model Validation Research](https://arxiv.org/abs/2405.00964)

---

## 🔄 **Next Steps**

1. **Explore the repo**: Clone and review the templates
2. **Choose your tier**: Solo (5) / Team (10) / Enterprise (15)
3. **Start with one command**: Try `/plan` on your next feature
4. **Build the habit**: Use artifacts consistently for 2 weeks
5. **Expand gradually**: Add one practice per week

---

## 🔄 **Cross-Model Review & Corrections**

This analysis was improved through cross-model review (comparing with analyses by Codex GPT-5, Claude Code Opus 4.6, and Cursor + Opus 4.6).

### What Was Added (Originally Missed):
1. **"Less Context" Review Principle** — Critical innovation about limiting reviewer context
2. **Cognitive Mode Specialization** — Agents organized by thinking mode, not task type
3. **Blameless System Improvement** — 5 Whys focuses on process gaps, not people
4. **Verification Gates** — Quality enforced structurally through mandatory checkpoints
5. **Make Implicit Explicit** — The unifying meta-principle behind all artifacts
6. **Ultimate Meta-Principle** — "Make good practices the path of least resistance"

### What Was Corrected:
- **Overstated**: Specific timelines for AI features (V1 weeks 1-4, etc.) → Replaced with principle-focused approach
- **Overstated**: Emoji progress tracking as "innovation" → Removed from key innovations (minor UX detail)
- **Added**: Measurement as a first principle (with actionable feedback loops)
- **Reframed**: Progressive autonomy as "earn trust through evidence" not prescriptive timeline

### Key Insight from Cross-Model Review:
The other analyses (especially Claude Code Opus 4.6) identified the **architectural principles** (cognitive modes, structural enforcement, implicit→explicit) that I initially missed by focusing too much on the **practice inventory**.

**Result**: This updated analysis now captures both the "what" (practices) and the "why" (architectural principles) of the system.

---

**Analysis by**: Claude Sonnet 4.5 (Anthropic)  
**Cross-reviewed with**: Codex GPT-5, Claude Code Opus 4.6, Cursor + Opus 4.6  
**Repository**: https://github.com/bennjph/agentic-ai-dev-team-setup  
**License**: MIT  
**Status**: Production-ready workflow template  
**Last Updated**: 2026-02-16 (v2 - cross-model reviewed)
