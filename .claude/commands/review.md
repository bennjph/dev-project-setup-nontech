# Code Review

Perform comprehensive code review of recent changes.

---

## Scope

Review code that was just written or modified. Focus on:
- Recent commits (if using git)
- Files mentioned in the active plan
- Any files the user specifies

---

## Review Checklist

### 1. Logging

❌ **Bad**:
- `console.log()` statements
- `print()` in production code
- Debug statements left in

✅ **Good**:
- Proper logging library with levels (debug, info, warn, error)
- Contextual log messages
- No sensitive data in logs

---

### 2. Error Handling

❌ **Bad**:
- No try-catch for async operations
- Silent failures (empty catch blocks)
- Generic error messages ("Error occurred")

✅ **Good**:
- Try-catch for all async functions
- Meaningful error messages for debugging
- Centralized error handlers
- User-friendly error messages for UI

---

### 3. TypeScript (if applicable)

❌ **Bad**:
- `any` types
- `@ts-ignore` comments
- Missing types on function parameters/returns

✅ **Good**:
- Proper type definitions
- Interfaces for objects
- Type guards where needed
- No implicit any

---

### 4. Production Readiness

❌ **Bad**:
- Hardcoded API keys or secrets
- TODO comments
- Debug flags left enabled
- Test data in production code

✅ **Good**:
- Environment variables for config
- All TODOs converted to issues
- Clean, shippable code
- No test/mock data

---

### 5. React/Hooks (if applicable)

❌ **Bad**:
- Missing cleanup in `useEffect`
- Incomplete dependency arrays
- Infinite render loops
- State updates in render

✅ **Good**:
- Effects have cleanup functions
- Dependencies complete and correct
- No unnecessary re-renders
- State updates in event handlers/effects only

---

### 6. Performance

❌ **Bad**:
- N+1 database queries
- Expensive calculations in render
- No memoization for heavy computations
- Large bundle sizes

✅ **Good**:
- Efficient queries
- `useMemo` / `useCallback` for expensive operations
- Code splitting where appropriate
- Optimized images/assets

---

### 7. Security

❌ **Bad**:
- No auth checks on protected routes
- Raw user input in queries (SQL injection risk)
- No input validation
- Exposed sensitive data in client

✅ **Good**:
- Auth middleware on protected endpoints
- Parameterized queries / ORM
- Input validation and sanitization
- Secrets only on server, never in client code

---

### 8. Architecture

❌ **Bad**:
- Code in wrong directory (breaks conventions)
- Circular dependencies
- God classes/functions (too much responsibility)
- Doesn't follow existing patterns

✅ **Good**:
- Follows project structure
- Clear separation of concerns
- Each function/component has single responsibility
- Consistent with existing codebase patterns

---

## Output Format

```markdown
## Code Review Results

### ✅ Looks Good

- Proper error handling throughout
- TypeScript types are well-defined
- Follows existing React patterns
- No security issues detected

---

### ⚠️ Issues Found

#### CRITICAL

- **[File:Line]** `src/api/users.ts:42` — SQL injection vulnerability
  - **Issue**: Raw user input used directly in query
  - **Fix**: Use parameterized queries or ORM
  - **Example**:
    ```typescript
    // Bad
    db.query(`SELECT * FROM users WHERE id = ${userId}`)
    
    // Good
    db.query('SELECT * FROM users WHERE id = $1', [userId])
    ```

#### HIGH

- **[File:Line]** `src/components/Dashboard.tsx:18` — Missing error boundary
  - **Issue**: Component can crash entire app
  - **Fix**: Wrap in ErrorBoundary component
  
- **[File:Line]** `src/lib/process.ts:55` — No try-catch on async function
  - **Issue**: Unhandled promise rejection possible
  - **Fix**: Add try-catch block

#### MEDIUM

- **[File:Line]** `src/components/QuizCard.tsx:103` — `any` type used
  - **Issue**: Loses type safety
  - **Fix**: Define proper interface for `question` object

- **[File:Line]** `src/utils/helpers.ts:22` — Console.log left in code
  - **Issue**: Debug statement in production code
  - **Fix**: Remove or replace with proper logger

#### LOW

- **[File:Line]** `src/components/Button.tsx:15` — Magic number
  - **Issue**: Hardcoded `300` for timeout
  - **Fix**: Extract to named constant `DEBOUNCE_DELAY = 300`

---

### 📊 Summary

- **Files reviewed**: 8
- **Critical issues**: 1
- **High issues**: 2
- **Medium issues**: 2
- **Low issues**: 1

---

### Recommended Actions

**Before shipping**:
1. ❗ **MUST FIX**: Critical SQL injection issue
2. ⚠️ **SHOULD FIX**: Missing error handling (2 issues)
3. ✨ **NICE TO FIX**: Type safety and code quality (3 issues)

**Next step**: Fix critical and high issues, then run `/peer-review` for cross-model validation.
```

---

## Severity Levels

| Level | When to Use | Examples |
|-------|-------------|----------|
| **CRITICAL** | Security, data loss, crashes | SQL injection, exposed secrets, auth bypass |
| **HIGH** | Bugs, bad UX, performance issues | Unhandled errors, memory leaks, infinite loops |
| **MEDIUM** | Code quality, maintainability | Type safety, missing tests, code organization |
| **LOW** | Style, minor improvements | Magic numbers, inconsistent naming, comments |

---

## Review Process

1. **Read the code** thoroughly (don't skim)
2. **Check each category** from the checklist
3. **For each issue found**:
   - Document severity
   - Explain the problem
   - Suggest specific fix
   - Provide code example if helpful
4. **Summarize findings**
5. **Recommend next steps**

---

## Red Flags (Always Call Out)

These are CRITICAL — stop and fix immediately:

🚨 Hardcoded API keys or secrets  
🚨 SQL injection vulnerabilities  
🚨 Auth bypass or broken access control  
🚨 User data exposed in logs  
🚨 Infinite loops or recursion without base case  
🚨 Memory leaks (event listeners not removed)  

---

## After Review

**If CRITICAL issues found**:
> "⚠️ **CRITICAL ISSUES DETECTED**
> 
> Do NOT ship this code. Fix critical issues first.
> 
> Critical issue: [brief description]
> 
> Fix this, then run `/review` again."

**If HIGH issues found**:
> "⚠️ High-priority issues found. 
> 
> Recommend fixing before shipping, but not blocking.
> 
> Next step: Fix high issues, then `/peer-review` for validation."

**If only MEDIUM/LOW issues**:
> "✅ Code looks good overall. 
> 
> [X] medium/low issues found but not blocking.
> 
> Next step: Run `/peer-review` for cross-model validation."

**If no issues**:
> "✅ Excellent! No issues found.
> 
> Code is clean, secure, and follows best practices.
> 
> Next step: Run `/peer-review` for cross-model validation."

---

## Persist Review to Plan File

**After completing the review**, append a summary to the active plan file under a `## Review Log` section:

```markdown
## Review Log

### Self-Review — [YYYY-MM-DD]

- **Files reviewed**: [count]
- **Verdict**: [SHIP / FIX REQUIRED / BLOCKED]
- **Critical**: [count] — [one-line summary if any]
- **High**: [count] — [one-line summary if any]
- **Medium**: [count]
- **Low**: [count]
- **Action**: [What was done — e.g., "Fixed 1 critical, 2 high. Re-reviewed clean."]
```

This ensures there's a durable record that review happened and what it found, even after the chat session ends.

---

**Remember**: You wrote this code, so you might miss your own mistakes. That's why `/peer-review` (different model) comes next.
