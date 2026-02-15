# Project Setup Instructions

**How to use this AI-native development template**

---

## Prerequisites

Before using this template, you need **at least one AI tool**. Here's how to get set up:

### Option 1: Cursor (Recommended for Beginners)

**Why Cursor**: All-in-one solution with AI built-in. Best for non-technical users.

1. **Download Cursor**: https://cursor.com
2. **Sign up for Cursor Pro** ($20/mo):
   - Open Cursor → Settings → Subscription
   - Click "Upgrade to Pro"
   - Includes Claude Opus, GPT-4, and Cursor Composer
3. **Done!** Cursor is ready to use with this template.

**Cost**: $20/mo (includes everything)

---

### Option 2: VS Code + Claude Code Extension

**Why this**: If you prefer VS Code and want to use Anthropic's Claude models.

1. **Download VS Code**: https://code.visualstudio.com
2. **Get Claude Pro** ($20/mo):
   - Go to https://claude.ai/settings/billing
   - Subscribe to Claude Pro
3. **Install Claude Code extension**:
   - Open VS Code Extensions (Cmd+Shift+X)
   - Search "Claude Code" by Anthropic
   - Click Install
4. **Sign in**: Extension will prompt you to authenticate with your Claude Pro account

**Cost**: $20/mo Claude Pro

---

### Option 3: VS Code + GitHub Copilot (Codex)

**Why this**: If you prefer OpenAI's models or already have GitHub Copilot.

1. **Download VS Code**: https://code.visualstudio.com
2. **Get ChatGPT Plus** ($20/mo):
   - Go to https://chatgpt.com/
   - Subscribe to ChatGPT Plus
3. **Install GitHub Copilot**:
   - Open VS Code Extensions (Cmd+Shift+X)
   - Search "GitHub Copilot"
   - Click Install
   - Sign in with GitHub account (needs Copilot subscription or ChatGPT Plus)

**Cost**: $20/mo ChatGPT Plus

---

### Multi-Tool Setup (Advanced)

**For cross-model peer review** (recommended after you're comfortable):

Combine tools for better results:
- **Cursor Pro ($20)** + **Claude Pro ($20)** = $40/mo
- Use Cursor for main work, Claude Code for peer review
- Different models catch different bugs

**Most users start with just Cursor Pro** and add more tools later.

---

## What This Kit Contains

A complete project template for building with AI (Claude Code, Cursor, Codex).

**Key features**:
- ✅ **8 slash commands** for phased development workflow
- ✅ **Multi-tool support** (Claude Code + Cursor + Codex)
- ✅ **Persistent CTO context** (project folder IS the CTO)
- ✅ **AI-native documentation** structure
- ✅ **Cross-model peer review** process

**Based on**: Zevi Arnovitz's workflow (Meta PM) adapted for multiple AI tools.

---

## Quick Start

### 1. Copy Template to New Project

```bash
# Copy the entire project-kit folder
cp -r project-kit/ ~/projects/my-new-project/

# Or start from an existing project
cp -r project-kit/* ~/projects/existing-project/
```

### 2. Customize `CLAUDE.md`

Edit `CLAUDE.md` and replace all `[PLACEHOLDERS]`:

- [ ] `[PROJECT NAME]` → Your project name
- [ ] `[One sentence description]` → What your project does
- [ ] Tech stack section → Your actual stack
- [ ] Quality standards → Your project-specific rules

**Critical sections** to customize:
- Identity (lines 7-12)
- Tech Stack (lines 21-34)
- Project-Specific Rules (lines 270-280)

### 3. Customize Documentation Templates

Edit these files:

- [ ] `docs/ARCHITECTURE.md` → Your system design
- [ ] `docs/TECH-STACK.md` → Your technology choices
- [ ] `docs/WORKFLOW.md` → Any workflow customizations (usually leave as-is)

**Don't overthink** — these will evolve as you build.

### 4. Open Project in Your Tool

**If using Cursor**:
```bash
cd ~/projects/my-new-project
cursor .
```

**If using VS Code**:
```bash
cd ~/projects/my-new-project
code .
```

### 5. Verify Your Tool Reads the Config Files

**Test in Cursor**:
1. Open Cursor chat (Cmd+L or Ctrl+L)
2. Type `/` and you should see the 8 custom commands
3. Ask "What project am I working on?" — it should know from `CLAUDE.md`

**Test in Claude Code extension (VS Code)**:
1. Open Claude Code panel
2. Ask "What project am I working on?" — it should read from `CLAUDE.md`
3. Type `/` to see custom commands from `.claude/commands/`

**Test in GitHub Copilot (VS Code)**:
1. Open Copilot chat
2. It will read context from `AGENTS.md` when you ask coding questions

### 6. Understanding Which File Each Tool Reads

| Tool | What It Reads | Purpose |
|------|---------------|---------|
| **Cursor** | `.cursorrules` → points to `CLAUDE.md` | Main instructions + slash commands from `.cursor/commands/` |
| **Claude Code extension** | `CLAUDE.md` directly | Main instructions + slash commands from `.claude/commands/` |
| **GitHub Copilot/Codex** | `AGENTS.md` → points to `CLAUDE.md` | Reads project context for coding help |

**All tools end up reading the same project context** — just through different entry points. This means your AI always knows your project, no matter which tool you use.

---

## Using the Workflow

### Your First Feature

1. **Capture the idea**:
   ```
   /create-issue
   ```
   Describe your feature/bug. AI creates `docs/backlog/[issue].md`.

2. **Explore thoroughly**:
   ```
   /explore docs/backlog/[issue].md
   ```
   AI analyzes codebase and asks clarifying questions. Answer until no more questions.

3. **Create plan**:
   ```
   /create-plan
   ```
   AI generates `plans/[feature]-plan.md` with progress tracking.

4. **Review and approve** the plan

5. **Execute**:
   ```
   /execute
   ```
   AI implements step-by-step, updating plan as it goes.

6. **Self-review**:
   ```
   /review
   ```
   AI checks for bugs, security issues, quality problems.

7. **Peer review** (cross-model):
   - Switch to Codex: "Review all code changes"
   - Copy findings
   - Switch back to Claude Code:
     ```
     /peer-review
     [Paste Codex findings]
     ```
   - AI validates each finding (rejects false positives)

8. **Update docs**:
   ```
   /document
   ```
   AI updates `docs/ARCHITECTURE.md`, `docs/TECH-STACK.md`, plan status.

9. **Ship it!**

### Learning Concepts

Anytime something is confusing:

```
/learn [topic]

Examples:
/learn React Server Components
/learn how our auth system works
/learn why we chose Zustand over Redux
```

AI explains in 3 levels (Core → Mechanics → Deep Dive).

---

## Multi-Model Workflow

### Which Model for Which Task?

| Task | Use | Why |
|------|-----|-----|
| **Planning, Exploration** | Claude Code | Best at asking questions, understanding context |
| **Main Development** | Claude Code | Communicative, explains decisions |
| **Fast Simple Tasks** | Cursor Composer | Blazing fast for boilerplate |
| **Debugging Hard Bugs** | Codex (GPT) | Deep problem-solving |
| **Peer Review** | Different model than builder | Cross-model validation |
| **UI/Frontend** | Gemini (optional) | Great visual results |

### How to Switch Models

**In Cursor**:
- Bottom right: Click model name → Select different model
- Or use Composer vs Chat (different capabilities)

**In VS Code**:
- Switch between Claude Code extension and Codex extension
- Each reads its own config file

**Key**: All tools read the SAME project files, so context is shared.

---

## File Structure

```
my-project/
│
├── CLAUDE.md                    ← Main CTO prompt (source of truth)
├── .cursorrules                 ← Cursor config (points to CLAUDE.md)
├── AGENTS.md                    ← Codex config (points to CLAUDE.md)
│
├── .claude/commands/            ← Slash commands for Claude Code
│   ├── create-issue.md
│   ├── explore.md
│   ├── create-plan.md
│   ├── execute.md
│   ├── review.md
│   ├── peer-review.md
│   ├── document.md
│   └── learn.md
│
├── .cursor/commands/            ← Same commands for Cursor
│   └── (mirrors .claude/commands/)
│
├── docs/
│   ├── ARCHITECTURE.md          ← System design
│   ├── TECH-STACK.md            ← Technology choices
│   ├── WORKFLOW.md              ← How we work
│   ├── decisions/               ← ADRs (Architecture Decision Records)
│   │   └── (empty initially)
│   └── backlog/                 ← Issues (from /create-issue)
│       └── (empty initially)
│
├── plans/                       ← Execution plans (from /create-plan)
│   └── (empty initially)
│
├── SETUP.md                     ← This file
└── README.md                    ← Project description
```

---

## Maintaining Slash Commands

### Note on `.claude/commands/` vs `.cursor/commands/`

These directories contain **identical content**.

**Why two directories?**
- Claude Code extension reads `.claude/commands/`
- Cursor reads `.cursor/commands/`

**Options to keep in sync**:

1. **Manual** (current setup): Copy changes between directories
2. **Symlink** (advanced):
   ```bash
   rm -rf .cursor/commands
   ln -s .claude/commands .cursor/commands
   ```
3. **Single directory** (simplest): Only keep `.claude/commands/`, tell Cursor users to add this path in settings

**Recommendation**: Start with manual copies. Optimize later if needed.

---

## Customization Tips

### Adding Project-Specific Rules

Edit `CLAUDE.md` section "Project-Specific Rules" (line ~275):

```markdown
## Project-Specific Rules

- "Never modify database schema without creating migration"
- "All API endpoints must have OpenAPI docs"
- "UI components must be added to Storybook"
- [Your rule here]
```

### Adding New Slash Commands

1. Create new command file: `.claude/commands/my-command.md`
2. Use existing commands as templates
3. Mirror to `.cursor/commands/my-command.md`
4. Reference in `CLAUDE.md` "Slash Commands Available" section

### Adapting for Your Tech Stack

If using different tech stack:

1. Update `CLAUDE.md` "Tech Stack" section
2. Update `docs/TECH-STACK.md`
3. Update quality standards in `CLAUDE.md` (e.g., Python instead of TypeScript)
4. Update review checklist in `.claude/commands/review.md`

---

## Troubleshooting

### "Slash commands not working"

**Check**:
- Are you using the right tool? (Claude Code reads `.claude/`, Cursor reads `.cursor/`)
- Did you create the command files in the right directory?
- Try typing `/` to see available commands

**Solution**: Restart your editor after adding new commands.

### "AI doesn't remember project context"

**Check**:
- Does `CLAUDE.md` exist in project root?
- Is `CLAUDE.md` customized for your project (not still `[PLACEHOLDERS]`)?
- Did you restart the AI extension after adding `CLAUDE.md`?

**Solution**: Close and reopen the project in your editor.

### "Commands contradict each other"

**Remember**: `CLAUDE.md` is the source of truth.

If `.cursorrules` or `AGENTS.md` contradict `CLAUDE.md`, fix them to point to `CLAUDE.md`.

### "Which config file does my tool read?"

| Tool | Primary File | Secondary File |
|------|--------------|----------------|
| Claude Code extension | `CLAUDE.md` | `.claude/commands/` |
| Cursor AI | `.cursorrules` | `.cursor/commands/` |
| Codex/OpenAI | `AGENTS.md` | (none) |
| OpenCode | `AGENTS.md` | `.opencode/commands/` |

**Note**: Codex/OpenAI behavior is TBD — verify which file it actually reads.

---

## Advanced: Linear Integration

This template uses `docs/backlog/` for markdown issues.

**To upgrade to Linear**:

1. Add Linear MCP server (Anthropic's Model Context Protocol)
2. Update `/create-issue` command to use Linear API instead of markdown
3. Keep markdown as fallback for offline work

**See**: https://github.com/modelcontextprotocol/servers for Linear integration.

---

## Tips for Teams

This template is designed for **solo developers** building with AI.

**For teams**:
- Keep `CLAUDE.md` in version control (git)
- Team agrees on quality standards
- Add team-specific rules to `CLAUDE.md`
- Use Linear/GitHub Issues instead of `docs/backlog/`

---

## Next Steps

1. ✅ Customize `CLAUDE.md` for your project
2. ✅ Customize `docs/` templates
3. ✅ Run `/create-issue` to capture your first feature
4. ✅ Run `/explore` to analyze it
5. ✅ Run `/create-plan` to plan implementation
6. ✅ Run `/execute` to build it
7. ✅ Run `/review` + `/peer-review` to validate
8. ✅ Run `/document` to update docs
9. ✅ Ship it!

---

## Questions?

**Check these files for more info**:
- `README.md` — What this template is
- `CLAUDE.md` — Complete CTO context
- `docs/WORKFLOW.md` — Detailed workflow guide

**Stuck?** Run `/learn [topic]` to understand complex concepts.

---

**Good luck building!** 🚀

This template is based on real workflows used by Meta PMs to ship production apps with AI. You're in good hands.
