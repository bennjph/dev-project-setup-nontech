# [PROJECT NAME] — Architecture

> **TEMPLATE**: Replace [placeholders] with your project details.

---

## Overview

[2-3 sentences describing what this project does]

**Example**:
> StudyMate is a web app that helps students create custom quizzes from their study materials. Users upload PDFs, select pages, and the AI generates interactive tests with multiple choice and fill-in-the-blank questions.

---

## System Diagram

```
[High-level component diagram]

Example:

┌─────────────┐
│   Browser   │
│  (React UI) │
└──────┬──────┘
       │ HTTP
       ▼
┌─────────────┐
│   Backend   │
│  (Next.js)  │
└──────┬──────┘
       │
       ├──────► Database (Supabase)
       ├──────► AI Service (OpenAI)
       └──────► Storage (S3)
```

---

## Key Components

**Customize this for your project**:

### Frontend
- **`src/app/`**: Next.js app router pages
- **`src/components/`**: Reusable React components
- **`src/hooks/`**: Custom React hooks
- **`src/lib/`**: Utility functions and helpers

### Backend
- **`src/api/`**: API routes
- **`src/services/`**: Business logic (AI, database, auth)
- **`src/middleware/`**: Auth, logging, error handling

### Data
- **`src/types/`**: TypeScript type definitions
- **`prisma/schema.prisma`**: Database schema
- **`supabase/migrations/`**: Database migrations

---

## Data Model

**Key entities and relationships**:

**Example**:
```
User
├── id (uuid)
├── email (string)
├── name (string)
└── created_at (timestamp)

Quiz
├── id (uuid)
├── user_id (uuid) → User
├── title (string)
├── questions (json[])
└── created_at (timestamp)

QuizAttempt
├── id (uuid)
├── quiz_id (uuid) → Quiz
├── user_id (uuid) → User
├── score (number)
└── completed_at (timestamp)
```

---

## API / Integrations

**External services used**:

| Service | Purpose | Key Files |
|---------|---------|-----------|
| Supabase | Database + Auth | `src/lib/supabase.ts` |
| OpenAI | Quiz generation | `src/services/ai/generateQuiz.ts` |
| Stripe | Payments | `src/services/payments/` |
| Sentry | Error tracking | `src/lib/sentry.ts` |

---

## Critical Areas

**Areas that need careful handling**:

### `src/services/payments/`
- **Why**: Handles real money, must be secure
- **Rules**: 
  - Never store card details (use Stripe tokens)
  - All transactions logged
  - Webhook signature verification required

### `src/middleware/auth.ts`
- **Why**: Protects all user data
- **Rules**:
  - All protected routes use `withAuth()` wrapper
  - JWT tokens expire after 1 hour
  - Refresh tokens expire after 7 days

### `src/services/ai/`
- **Why**: Calls cost money, must prevent abuse
- **Rules**:
  - Rate limiting: 10 requests per hour per user
  - Cost tracking in database
  - Timeout after 30 seconds

---

## Deployment

**Where this runs**:

- **Frontend**: Vercel (automatic from `main` branch)
- **Database**: Supabase (hosted Postgres)
- **File Storage**: Supabase Storage
- **Monitoring**: Sentry for errors, Vercel Analytics

**Environments**:
- **Production**: `main` branch → https://app.example.com
- **Staging**: `staging` branch → https://staging.example.com
- **Local**: `localhost:3000`

---

## Decision Log

**Major architectural decisions** (see `docs/decisions/` for full ADRs):

- **ADR 001**: Why Next.js over Create React App
- **ADR 002**: Why Supabase over Firebase
- **ADR 003**: Why Zustand over Redux

---

## Getting Started (For AI Agents)

**Read these files first**:
1. `CLAUDE.md` — Full context and CTO role
2. `docs/TECH-STACK.md` — Technology choices
3. `docs/WORKFLOW.md` — How we work

**Before making changes**:
- Check `plans/` for active work
- Check `docs/backlog/` for planned features
- Run `/explore` to understand the change thoroughly
