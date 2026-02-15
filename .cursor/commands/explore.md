# Exploration Phase

**Your task is NOT to implement — only to understand and prepare.**

---

## Mission

Deeply analyze the problem before any code is written.

1. **Understand** the current codebase state
2. **Identify** all affected files and systems
3. **Map** dependencies and edge cases
4. **Ask** ALL clarifying questions
5. **Challenge** assumptions if something seems wrong

**NO CODE WRITING** during this phase.

---

## Process

### Step 1: Read the Request

If the user provided an issue file (e.g., `docs/backlog/[issue].md`), read it first.

If verbal request, confirm what you heard:
> "I understand you want to [summary]. Is that correct?"

### Step 2: Analyze the Codebase

1. **Find relevant files**:
   - Where would this feature live?
   - What existing code does similar things?
   - What files will need to be modified?

2. **Understand current architecture**:
   - How is this system currently structured?
   - What patterns are being used?
   - Are there any constraints or dependencies?

3. **Map dependencies**:
   - What other systems/components are affected?
   - Are there database changes needed?
   - Are there API changes needed?

4. **Identify edge cases**:
   - What could go wrong?
   - What user scenarios need handling?
   - Are there performance concerns?

### Step 3: Compile Understanding

Present your findings:

```markdown
## Current Understanding

[Describe what you found in the codebase]

## Key Areas Identified

- **File 1**: `path/to/file.ts` — [what it does, why it matters]
- **File 2**: `path/to/file.ts` — [what it does, why it matters]
- **System**: [system name] — [how it's affected]

## Current Architecture Pattern

[Describe the existing pattern you'll follow]

## Dependencies

- [Dependency 1]: [Why it matters]
- [Dependency 2]: [Why it matters]

## Edge Cases to Handle

1. [Edge case 1]
2. [Edge case 2]
3. [Edge case 3]
```

### Step 4: Ask Clarifying Questions

List ALL questions and ambiguities:

```markdown
## Clarifying Questions

**Scope**:
- [Question about feature scope]

**Data Model**:
- [Question about data structure]

**UX/UI**:
- [Question about user experience]

**Technical**:
- [Question about implementation approach]

**Validation**:
- [Question about how to validate/test]
```

---

## Rules

- **Do NOT write any code** — this is exploration only
- **Do NOT assume** requirements beyond what's stated
- **Ask questions** until you have zero ambiguity
- **Challenge** the user's assumptions if approach seems flawed
- **Go back and forth** until you have no more questions

---

## Red Flags to Watch For

If you notice these, SPEAK UP:

- Approach seems overly complex
- Breaking existing patterns without good reason
- Security concerns (auth, data exposure)
- Performance issues (N+1 queries, expensive operations)
- Breaking changes to existing features
- Missing error handling strategy

**Better to catch problems now than after implementation.**

---

## Example Interaction

**User**: "Add fill-in-the-blank questions to the quiz system"

**You**: 
> "Let me analyze the codebase...
> 
> **Current Understanding**:
> - Quiz system currently supports multiple-choice only
> - Questions are stored in `QuizQuestion` type
> - Question generation happens in `generateQuiz()`
> - UI renders in `QuizCard` component
> 
> **Key Files**:
> - `types/quiz.ts` — Need to extend `QuizQuestion` type
> - `lib/generateQuiz.ts` — Add fill-in-blank generation logic
> - `components/QuizCard.tsx` — Add new UI for blanks
> 
> **Clarifying Questions**:
> 
> 1. **Percentage**: You said 30% of questions. Should this be:
>    - Exactly 30% (strict)?
>    - Approximately 30% (flexible)?
> 
> 2. **Blanks per question**: You mentioned 2 blanks. Always 2, or range (1-3)?
> 
> 3. **Answer pool**: 6 potential answers total, 2 correct. Are the 4 incorrect answers:
>    - Random words from the text?
>    - AI-generated distractors?
> 
> 4. **UI interaction**: Drag-and-drop. Should users be able to:
>    - Drag both correct answers to both blanks (any order)?
>    - Specific answer per blank (order matters)?
> 
> 5. **Validation**: When do we check if the answer is correct?
>    - After each blank is filled?
>    - After submit button?
> 
> 6. **Data model**: Does the existing `QuizQuestion` type support this, or do we need a new type (`FillInBlankQuestion`)?
> 
> Once you answer these, I'll create the implementation plan."

---

## Success Criteria

✅ You understand the current codebase  
✅ You know exactly which files to modify  
✅ You've identified all edge cases  
✅ You've asked every question you have  
✅ You've challenged any questionable approach  
✅ You're ready to create a concrete plan  

**Next step**: Once all questions are answered, run `/create-plan`.

---

**Remember**: Exploration prevents mistakes. Time spent here saves time debugging later.
