# AI-Native Project Template

**Build production apps with AI using a proven workflow**

This template provides a complete development system for building with AI tools (Claude Code, Cursor, Codex). Based on the workflow used by product managers at Meta to ship real features without traditional coding.

---

## 📺 Learn More

**Inspired by**: [Zevi Arnovitz](https://www.linkedin.com/in/zevi-arnovitz/) (Product Manager at Meta)

**Watch the podcast**: [The non-technical PM's guide to building with Cursor](https://www.youtube.com/watch?v=1em64iUFt3U) (1h 15min)  
**Read the show notes**: [Lenny's Newsletter](https://www.lennysnewsletter.com/p/zevi-arnovitz-cursor-workflow)

Zevi shares how he built [StudyMate](https://studymate.ai/) — a revenue-generating quiz app — as a non-technical PM using AI tools. This template adapts his workflow for multiple AI platforms.

---

## What's Included

✅ **3 config files** — Works with Claude Code, Cursor AI, and Codex simultaneously  
✅ **8 slash commands** — Enforced workflow from idea → shipped feature  
✅ **AI-native docs** — Architecture, tech stack, workflow guides  
✅ **Cross-model review** — Different AIs validate each other's work  
✅ **Progress tracking** — Markdown plans with emoji status (🟩🟨🟥)  

---

## Quick Start

```bash
# 1. Copy template to your project
cp -r project-kit/ ~/projects/my-new-project/
cd ~/projects/my-new-project/

# 2. Customize CLAUDE.md (replace [PLACEHOLDERS])
vim CLAUDE.md

# 3. Open in Cursor or VS Code
cursor .

# 4. Start building
# Run: /create-issue to capture your first feature
```

**Read**: `SETUP.md` for complete setup instructions.

---

## The 8-Phase Workflow

```
/create-issue  →  Capture idea/bug to backlog
/explore       →  Analyze problem, ask questions
/create-plan   →  Generate implementation plan
/execute       →  Build step-by-step
/review        →  Self-review for bugs
/peer-review   →  Cross-model validation
/document      →  Update architecture docs
/learn         →  Understand complex concepts
```

**See**: `docs/WORKFLOW.md` for detailed workflow guide.

---

## Why This Workflow?

**Problem**: AI coding tools are eager to write code without understanding the problem. This leads to bugs, rework, and frustration.

**Solution**: Force **planning before coding** using slash commands.

### Key Innovations

1. **Persistent CTO context** — Project folder IS the CTO (no separate ChatGPT window)
2. **Multi-tool support** — Claude Code + Cursor + Codex read same files
3. **Cross-model review** — Different models catch different bugs
4. **"Less context" framing** — Primary model validates peer findings (prevents false positives)
5. **Learning loops** — `/learn` command for understanding, not just executing

---

## What Makes This Different?

| Traditional Coding | Bolt/Lovable/Replit | This Template |
|-------------------|---------------------|---------------|
| Write code manually | "Vibe coding" (AI builds everything) | **Phased workflow with gates** |
| No AI assistance | Too eager to code | **Plan → Approve → Execute** |
| Code review by humans | No review | **Self-review + cross-model** |
| Manual documentation | No documentation | **Auto-update with `/document`** |
| Trial and error | Trial and error | **Exploration before coding** |

**Result**: Fewer bugs, faster iteration, better code quality.

---

## File Structure

```
your-project/
├── CLAUDE.md              ← CTO system prompt (main config)
├── .cursorrules           ← Cursor config
├── AGENTS.md              ← Codex/OpenCode config
├── .claude/commands/      ← Slash commands (8 files)
├── .cursor/commands/      ← Same commands for Cursor
├── docs/
│   ├── ARCHITECTURE.md    ← System design
│   ├── TECH-STACK.md      ← Technology choices
│   ├── WORKFLOW.md        ← How we work
│   ├── decisions/         ← ADRs
│   └── backlog/           ← Issues (markdown)
├── plans/                 ← Execution plans
├── SETUP.md               ← Setup instructions
└── README.md              ← This file
```

---

## Who Is This For?

✅ **Non-technical PMs** who want to build products  
✅ **Solo founders** building MVPs with AI  
✅ **Junior engineers** learning to build with AI  
✅ **Technical PMs** who want better AI workflows  
✅ **Anyone** building side projects with AI tools  

❌ **Not for**: Large engineering teams (unless they adapt it)

---

## Requirements

**Tools** (at least one):
- Cursor (recommended) — https://cursor.com
- VS Code with Claude Code extension — https://marketplace.visualstudio.com
- VS Code with Codex/Copilot extension

**AI Subscriptions** (recommended):
- Claude Pro ($20/mo) — For Claude Code extension
- ChatGPT Plus ($20/mo) — For Codex extension (optional)
- Cursor Pro ($20/mo) — For Cursor Composer (optional)

**Total cost**: $20-60/mo depending on which tools you use.

---

## Example Projects Built This Way

This workflow was **inspired by** and **validated by** real projects:

- **StudyMate** (Zevi Arnovitz) — Quiz generation app, built solo, making revenue
- **Personal blogs** — Portfolio sites with CMS
- **Internal tools** — Automation dashboards
- **MVP products** — E-commerce, SaaS, marketplaces

**Time to first feature**: ~1-2 hours (including setup)

---

## Comparison to Other Templates

| Template | Focus | Multi-Tool | Workflow Enforcement | Learning Mode |
|----------|-------|------------|---------------------|---------------|
| **This** | Production apps | ✅ Yes (3 tools) | ✅ Yes (8 phases) | ✅ Yes (`/learn`) |
| T3 Stack | TypeScript setup | ❌ No | ❌ No | ❌ No |
| Create Next App | Basic Next.js | ❌ No | ❌ No | ❌ No |
| Bolt/Lovable | Vibe coding | ❌ No | ⚠️ Weak | ❌ No |

**This is the only template** that enforces phased development with multi-tool support.

---

## Tech Stack Agnostic

This template works with **any tech stack**:

✅ React, Vue, Svelte, or vanilla JS  
✅ Next.js, Remix, Astro, or SPA  
✅ TypeScript or JavaScript  
✅ Node, Python, Go, or any backend  
✅ PostgreSQL, MongoDB, Supabase, or any database  

Just customize `CLAUDE.md` and `docs/TECH-STACK.md` for your stack.

---

## Documentation

| File | Purpose |
|------|---------|
| **SETUP.md** | Complete setup guide (start here) |
| **CLAUDE.md** | CTO system prompt (customize this) |
| **docs/WORKFLOW.md** | Detailed workflow guide |
| **docs/ARCHITECTURE.md** | System design template |
| **docs/TECH-STACK.md** | Technology choices template |

---

## Contributing

This template is **open for adaptation**. Feel free to:

- Customize for your workflow
- Add new slash commands
- Improve existing prompts
- Share your improvements

**No formal contribution process** — this is a template, not a framework.

---

## Credits

**Inspired by**:
- Zevi Arnovitz (Meta PM) — Original workflow creator
- Lenny Rachitsky — Podcast host who shared Zevi's workflow
- Tal Raviv — Introduced Zevi to the podcast

**Adapted by**: The OpenCode M1 team

**Source**: [Lenny's Newsletter Podcast with Zevi Arnovitz](https://www.lennysnewsletter.com/)

---

## License

**Public Domain** — Use this however you want.

No attribution required. No restrictions.

---

## Support

**Questions?** Read `SETUP.md` for detailed instructions.

**Stuck?** Use the `/learn` command to understand concepts.

**Issues?** Check the "Troubleshooting" section in `SETUP.md`.

---

## What's Next?

1. Read `SETUP.md` for complete setup
2. Customize `CLAUDE.md` for your project
3. Run `/create-issue` to start building
4. Ship your first feature using the 8-phase workflow

**Good luck!** 🚀

---

**Note**: This is a template, not a framework. Adapt it to your needs. The workflow matters more than the tools.
