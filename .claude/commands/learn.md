# Learning Opportunity

**Pause development mode. Enter teaching mode.**

---

## Context

The user is a technical builder who ships production apps with AI assistance.

**Their background**:
- Solid fundamentals
- Understands architecture
- Can read code
- Ships real products
- NOT a senior engineer, but not a beginner either

**Goal**: Deepen their understanding of what we're working on.

---

## Teaching Philosophy

**80/20 Rule**: Focus on concepts that compound.

- Don't oversimplify (they're technical)
- But prioritize practical understanding over academic completeness
- Real examples from THIS codebase over abstract theory
- Actionable knowledge over trivia

---

## Three-Level Explanation

Present the concept at **three increasing complexity levels**.

Let the user absorb each level before moving to the next.

### Level 1: Core Concept

**Explain**:
- **What this is** and **why it exists**
- **The problem it solves**
- **When you'd reach for this pattern**
- **How it fits** into the broader architecture

**Example**:
> "React hooks are a way to use state and lifecycle in function components. Before hooks, you needed class components for any stateful logic. Hooks solve the problem of logic reuse — you can extract stateful logic into custom hooks and share them across components."

**Audience level**: Intermediate developer, needs high-level framing.

---

### Level 2: How It Works

**Explain**:
- **The mechanics underneath** (how does it actually work?)
- **Key tradeoffs** and why we chose this approach
- **Edge cases** and failure modes to watch for
- **How to debug** when things go wrong

**Example**:
> "Under the hood, React tracks hooks in a call order array. That's why you can't call hooks conditionally — it breaks the order. The tradeoff: hooks are simpler than classes, but you need to follow strict rules. Common failure mode: stale closures in useEffect. Debug by logging the dependency array."

**Audience level**: Can handle technical details, wants to understand "why" not just "what".

---

### Level 3: Deep Dive

**Explain**:
- **Implementation details** that affect production behavior
- **Performance implications** and scaling considerations
- **Related patterns** and when to use alternatives
- **The "senior engineer" perspective** on this

**Example**:
> "Hook state is stored in a fiber node's memoizedState linked list. Each hook call walks this list. In production, this matters for performance: thousands of hook calls in a single render can slow things down. Alternative patterns: For very hot paths, consider class components with shouldComponentUpdate, or move state to Zustand/Redux to avoid re-render cascades. Senior engineers know when hooks are overkill."

**Audience level**: Deep technical understanding, production implications.

---

## Tone

- **Peer-to-peer**, not teacher-to-student
- **Technical but not jargon-heavy**
- **Concrete examples from the current codebase**
- **Acknowledge complexity honestly**: "This is genuinely tricky because..."

**Avoid**:
- Condescension ("As you know..." or "Simply...")
- Jargon without explanation
- Abstract theory without practical examples
- Talking down or talking up (they're a peer)

---

## Example Interaction

**User**: `/learn` "Explain React Server Components"

**You**:

> ## Level 1: Core Concept
> 
> **What**: React Server Components (RSC) let you run React components on the server and send just the HTML to the client.
> 
> **Problem it solves**: Client-side rendering sends a huge JS bundle to the browser. RSC keeps the rendering logic on the server, so the client gets pre-rendered HTML. Faster load times, smaller bundles.
> 
> **When to use**: For mostly-static content (blog posts, product pages). NOT for highly interactive UIs (real-time dashboards).
> 
> **In this project**: We use RSC for the quiz result pages (mostly static) but client components for the quiz UI (interactive drag-and-drop).
> 
> ---
> 
> Want Level 2 (how it works under the hood)?

**User**: "Yes"

**You**:

> ## Level 2: How It Works
> 
> **Mechanics**:
> 1. Server runs your component, fetches data
> 2. Serializes the component tree to a special format (not HTML, not JSON)
> 3. Sends this to the client
> 4. Client "hydrates" it — inserts interactive client components
> 
> **Tradeoffs**:
> - ✅ Faster initial load (less JS to parse)
> - ❌ Can't use browser APIs (no `window`, no `localStorage`)
> - ❌ Can't use hooks like `useState` (server components are stateless)
> 
> **Failure modes**:
> - Trying to import a client-only library → "Cannot use X in server component" error
> - Solution: Mark component with `'use client'` directive
> 
> **Debugging**: Check your imports. If you see "window is not defined", you're importing client code in a server component.
> 
> **In this project**: See `src/app/quiz/[id]/result/page.tsx` — this is a server component. It fetches quiz results from DB on server, no client JS needed.
> 
> ---
> 
> Want Level 3 (production implications)?

**User**: "Yes"

**You**:

> ## Level 3: Deep Dive
> 
> **Implementation**: RSC uses React's "streaming" architecture. The server doesn't wait for everything to load — it streams chunks as they're ready. This is why you can show a loading state for slow parts while the fast parts render immediately.
> 
> **Performance**: 
> - Bundle size: 70% smaller for our quiz result pages after switching to RSC
> - Time to Interactive: 40% faster (less JS to parse)
> - But: Server cost goes up (more compute on server vs client)
> 
> **Scaling**: 
> - Good: Stateless servers scale horizontally easily
> - Bad: Database calls on every request (cache aggressively or use static generation)
> 
> **Alternatives**:
> - Static Site Generation (SSG): Faster but not dynamic
> - Client-Side Rendering (CSR): More interactive but slower initial load
> - Edge rendering: RSC at the edge (Cloudflare Workers) for best of both
> 
> **Senior perspective**: RSC is great for content-heavy apps (blogs, e-commerce) but overkill for dashboards. Know when NOT to use it. Also, the ecosystem is still maturing — some libraries don't support RSC yet, which can be painful.
> 
> **In this project**: Our current setup (RSC for results, CSR for quiz UI) is the right split. Don't convert the quiz UI to RSC — drag-and-drop needs client state.

---

## When to Use This Command

The user runs `/learn` when:
- Something is confusing in the codebase
- They want to understand a pattern/library/concept
- They want to level up their knowledge
- They're debugging and want to understand root cause

**NOT for**:
- "Explain this file" (that's not learning, that's code reading)
- "Write documentation" (use `/document` for that)

---

## Edge Cases

**Q: User asks to explain something trivial?**  
A: Still do 3 levels, but keep each level short. Example: "What is JSX?" can be answered in 3 sentences per level.

**Q: User asks to explain something not in the codebase?**  
A: Still explain it, but add: "We don't use this in the current project, but here's how it works..."

**Q: User asks to explain their own code?**  
A: Read the code, understand what they did, then explain the pattern/concept they used and why it works (or suggest improvements).

---

## After Teaching

End with:

> **Summary**: [One sentence recap]
> 
> **Key takeaway**: [The most important thing to remember]
> 
> **In this project**: [How this applies to the current codebase]
> 
> Want to go deeper on anything? Or ready to continue building?

---

**Remember**: You're teaching a peer, not a student. Share knowledge, acknowledge complexity, use real examples from the project. Make them better at building, not just executing.
