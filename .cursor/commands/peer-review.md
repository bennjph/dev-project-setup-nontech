# Peer Review

A different AI model has reviewed the code and provided findings.

**Your job**: Critically evaluate their findings, NOT blindly accept them.

---

## Critical Context

- **The peer reviewer has LESS context than you**
  - They didn't write the code
  - They didn't participate in exploration or planning
  - They may not fully understand the architecture
  
- **YOU are the dev lead on this project**
  - You made the architectural decisions
  - You understand the full context
  - You know what's intentional vs what's a bug

- **Your job**: Validate each finding
  - Is this actually an issue?
  - Or did the reviewer misunderstand?

---

## Input Format

The user will paste findings from another AI model (e.g., Codex, Cursor, Gemini):

```
[PASTE PEER REVIEW FINDINGS HERE]
```

Example:
```
Finding 1: Missing error handling in getUserData() function
Finding 2: Performance issue - unnecessary re-renders in Dashboard
Finding 3: Security risk - API key exposed in client code
```

---

## Process

For EACH finding from the peer review:

### Step 1: Verify It Exists

**Check the actual code** — does this issue really exist?

- Read the file and line number mentioned
- Understand what the code actually does
- Check if the finding is accurate

### Step 2: Evaluate Validity

**If the issue DOESN'T exist**:
- Explain why the reviewer is wrong
- Show the actual code that addresses this
- Example: "Already handled in error boundary at line 15"

**If the issue DOES exist**:
- Assess severity (CRITICAL, HIGH, MEDIUM, LOW)
- Decide if it needs fixing
- Add to fix plan

### Step 3: Consider Context

Ask yourself:
- Is this intentional by design?
- Is there context the reviewer doesn't have?
- Is this a real problem or a stylistic preference?

---

## Output Format

```markdown
## Peer Review Validation

### Valid Findings (Confirmed Issues)

#### CRITICAL
- **Finding**: [Peer's finding]
  - **Verified**: Yes, this is a real issue
  - **Location**: `src/path/file.ts:42`
  - **Fix Required**: [What needs to be done]

#### HIGH
- **Finding**: [Peer's finding]
  - **Verified**: Yes, needs fixing
  - **Location**: `src/path/file.ts:100`
  - **Fix Required**: [What needs to be done]

#### MEDIUM
- **Finding**: [Peer's finding]
  - **Verified**: Yes, minor issue
  - **Location**: `src/path/file.ts:55`
  - **Fix Optional**: [What could be improved]

---

### Invalid Findings (Rejected)

- **Finding**: "Missing error handling in getUserData()"
  - **Status**: ❌ Incorrect
  - **Reason**: Error handling is implemented via ErrorBoundary component at `src/components/ErrorBoundary.tsx:15`. The reviewer missed this because it's at the component tree level, not inline.
  - **Evidence**: See `src/App.tsx:22` where Dashboard is wrapped in ErrorBoundary

- **Finding**: "API key exposed in environment.ts"
  - **Status**: ❌ Incorrect  
  - **Reason**: This is a PUBLIC API key (clearly marked as `NEXT_PUBLIC_`), which is safe to expose client-side. The reviewer confused it with a secret key. Secret keys are in `.env.local` (not committed).

- **Finding**: "Should use TypeScript strict mode"
  - **Status**: ⚠️ Stylistic preference
  - **Reason**: We're using strict mode, it's configured in `tsconfig.json`. The reviewer may have been looking at an older file.

---

### Action Plan

**Immediate (before shipping)**:
1. Fix CRITICAL issue: [description]
2. Fix HIGH issue: [description]

**Follow-up (can ship without)**:
3. Consider MEDIUM improvements: [description]

**Total**: [X] valid findings, [Y] invalid findings

---

### Summary

**Peer review added value**: [Yes/Partially/No]

- **Caught real issues**: [X] critical, [Y] high  
- **False positives**: [Z] findings were incorrect/misleading  
- **Recommendations**: [Overall assessment]

**Next step**: Fix confirmed issues, then run `/review` again to verify fixes.
```

---

## Examples of Common False Positives

### Example 1: Missing Context

**Peer says**: "No authentication on this route"

**You verify**: 
```typescript
// src/middleware/auth.ts
export const protectedRoute = withAuth(handler)

// Reviewer missed that withAuth middleware handles auth
// Auth IS implemented, just not inline
```

**Your response**:
❌ Invalid — Auth is handled via `withAuth` middleware

### Example 2: Intentional Design

**Peer says**: "This function is too long (200 lines)"

**You verify**:
```typescript
// This is a generated parser function
// It's long because it handles 50 different token types
// Splitting it would make it LESS readable
```

**Your response**:
⚠️ Stylistic — Intentionally long for code generation clarity

### Example 3: Already Fixed

**Peer says**: "Missing type definition for User"

**You verify**:
```typescript
// types/user.ts
export interface User {
  id: string
  name: string
  email: string
}

// Reviewer was looking at old code or wrong file
```

**Your response**:
❌ Invalid — Type exists in `types/user.ts`

---

## When to Push Back vs Accept

### Accept the finding when:
✅ Issue actually exists in the code  
✅ Severity is accurately assessed  
✅ Fix would improve code quality/security  
✅ Reviewer identified something you missed  

### Push back when:
❌ Issue doesn't exist (reviewer misread code)  
❌ Context is missing (handled elsewhere)  
❌ Intentional design decision  
❌ Stylistic preference, not a real problem  
❌ Already fixed (reviewer has stale info)  

---

## Red Flags in Peer Reviews

Watch for these signs that the peer reviewer didn't understand the codebase:

🚩 Suggesting to add code that already exists  
🚩 Flagging intentional design patterns as "wrong"  
🚩 Not understanding the framework/library conventions  
🚩 Recommending changes that would break functionality  
🚩 Nitpicking style without understanding context  

When you see these, **push back with evidence**.

---

## After Validation

**If critical/high issues confirmed**:
> "⚠️ Peer review found [X] real issues ([Y] critical, [Z] high).
> 
> **Action plan**:
> 1. Fix: [critical issue]
> 2. Fix: [high issue]
> 
> Fixing these now, then will run `/review` again."

**If only false positives**:
> "✅ Reviewed all peer findings.
> 
> **Result**: All [X] findings were false positives or context misunderstandings.
> 
> - [X] issues already handled
> - [Y] issues were intentional design
> - [Z] issues don't exist in code
> 
> Code is good to proceed. Next: `/document`"

**If mix of valid and invalid**:
> "📊 Peer review analysis:
> 
> **Valid**: [X] issues confirmed  
> **Invalid**: [Y] false positives  
> 
> Fixing the [X] valid issues now."

---

**Remember**: Peer review is valuable but not infallible. The peer reviewer is helping you catch blind spots, but YOU are the expert on this code. Trust your understanding, but stay open to legitimate issues.
