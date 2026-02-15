# Tech Stack

> **TEMPLATE**: Customize for your project. Delete sections that don't apply.

---

## Core

- **Language**: [TypeScript, Python, Go, etc.]
- **Runtime**: [Node.js, Bun, Deno, etc.]
- **Package Manager**: [npm, pnpm, yarn, bun, etc.]

**Example**:
- **Language**: TypeScript 5.0
- **Runtime**: Node.js 20
- **Package Manager**: pnpm

---

## Frontend

- **Framework**: [React, Vue, Svelte, etc.]
- **Meta-Framework**: [Next.js, Remix, Astro, etc.]
- **Styling**: [Tailwind, CSS Modules, styled-components, etc.]
- **UI Components**: [shadcn/ui, Material-UI, Chakra, etc.]

**Example**:
- **Framework**: React 18
- **Meta-Framework**: Next.js 14 (App Router)
- **Styling**: Tailwind CSS
- **UI Components**: shadcn/ui

---

## State Management

- **Global State**: [Zustand, Redux, Jotai, Context, etc.]
- **Server State**: [React Query, SWR, tRPC, etc.]
- **Form State**: [React Hook Form, Formik, etc.]

**Example**:
- **Global State**: Zustand (lightweight, minimal boilerplate)
- **Server State**: React Query (caching, refetching)
- **Form State**: React Hook Form

---

## Backend

- **Framework**: [Express, Fastify, Hono, etc.]
- **API Style**: [REST, GraphQL, tRPC, etc.]
- **Validation**: [Zod, Yup, Joi, etc.]

**Example**:
- **Framework**: Next.js API Routes
- **API Style**: REST
- **Validation**: Zod

---

## Database

- **Database**: [PostgreSQL, MySQL, MongoDB, etc.]
- **ORM/Query Builder**: [Prisma, Drizzle, TypeORM, Knex, etc.]
- **Migrations**: [Prisma Migrate, Drizzle Kit, etc.]
- **Hosting**: [Supabase, PlanetScale, Railway, etc.]

**Example**:
- **Database**: PostgreSQL 15
- **ORM**: Prisma
- **Migrations**: Prisma Migrate
- **Hosting**: Supabase

---

## Authentication

- **Provider**: [Supabase Auth, NextAuth, Clerk, Auth0, etc.]
- **Strategy**: [JWT, session, OAuth, etc.]

**Example**:
- **Provider**: Supabase Auth
- **Strategy**: JWT with refresh tokens
- **Social**: Google, GitHub

---

## File Storage

- **Provider**: [Supabase Storage, AWS S3, Cloudflare R2, etc.]
- **CDN**: [Cloudflare, AWS CloudFront, etc.]

**Example**:
- **Provider**: Supabase Storage
- **CDN**: Supabase CDN (automatic)

---

## AI / LLMs

- **Provider**: [OpenAI, Anthropic, Gemini, etc.]
- **SDK**: [OpenAI SDK, Vercel AI SDK, LangChain, etc.]
- **Models**: [Which models for which tasks]

**Example**:
- **Provider**: OpenAI
- **SDK**: OpenAI Node.js SDK
- **Models**:
  - `gpt-4o` for quiz generation
  - `gpt-3.5-turbo` for simple completions

---

## Payments

- **Provider**: [Stripe, PayPal, Paddle, etc.]
- **Integration**: [Checkout, Elements, etc.]

**Example**:
- **Provider**: Stripe
- **Integration**: Stripe Checkout (hosted)
- **Webhooks**: Yes (for subscription updates)

---

## Email

- **Provider**: [Resend, SendGrid, Postmark, etc.]
- **Templates**: [React Email, MJML, HTML, etc.]

**Example**:
- **Provider**: Resend
- **Templates**: React Email

---

## Analytics

- **Product Analytics**: [PostHog, Mixpanel, Amplitude, etc.]
- **Web Analytics**: [Vercel Analytics, Plausible, etc.]
- **Error Tracking**: [Sentry, Rollbar, etc.]

**Example**:
- **Product**: PostHog (self-hosted)
- **Web**: Vercel Analytics
- **Errors**: Sentry

---

## Infrastructure

- **Hosting**: [Vercel, Railway, Render, AWS, etc.]
- **CI/CD**: [GitHub Actions, Vercel, GitLab CI, etc.]
- **Secrets**: [Vercel Env, AWS Secrets Manager, etc.]
- **Monitoring**: [Vercel, Sentry, Datadog, etc.]

**Example**:
- **Hosting**: Vercel (frontend + API)
- **Database Hosting**: Supabase
- **CI/CD**: Vercel (automatic on push to `main`)
- **Secrets**: Vercel Environment Variables
- **Monitoring**: Sentry + Vercel Logs

---

## Development Tools

- **AI Coding**: [Claude Code, Cursor, Codex, etc.]
- **Linting**: [ESLint, Biome, etc.]
- **Formatting**: [Prettier, Biome, etc.]
- **Type Checking**: [tsc, etc.]
- **Testing**: [Vitest, Jest, Playwright, etc.]

**Example**:
- **AI Coding**: 
  - Claude Code (primary - planning, development)
  - Cursor Composer (fast tasks)
  - Codex (debugging, peer review)
- **Linting**: ESLint (with TypeScript rules)
- **Formatting**: Prettier
- **Type Checking**: TypeScript strict mode
- **Testing**: Vitest (unit), Playwright (e2e)

---

## Key Dependencies

**Most important packages** (full list in `package.json`):

| Package | Version | Purpose |
|---------|---------|---------|
| `next` | 14.x | React meta-framework |
| `react` | 18.x | UI library |
| `typescript` | 5.x | Type safety |
| `tailwindcss` | 3.x | Styling |
| `@supabase/supabase-js` | 2.x | Database + Auth |
| `openai` | 4.x | AI integration |
| `zod` | 3.x | Runtime validation |
| `zustand` | 4.x | State management |

---

## Why These Choices?

See `docs/decisions/` for full ADRs (Architecture Decision Records).

**Quick rationale**:

- **Next.js**: Best React meta-framework, great DX, Vercel integration
- **TypeScript**: Type safety prevents bugs, better DX
- **Tailwind**: Fast styling, no CSS files, consistent design
- **Supabase**: PostgreSQL + Auth + Storage in one, great DX
- **Zustand**: Simpler than Redux, sufficient for our needs
- **Prisma**: Best TypeScript ORM, migrations built-in

---

## Updating This File

When tech stack changes:
- ✅ New dependency added → Add to "Key Dependencies"
- ✅ Framework upgraded → Update version number
- ✅ Tool replaced (e.g., Jest → Vitest) → Update and explain why in ADR
- ✅ New service integrated → Add to relevant section

Run `/document` after any stack changes to keep this current.
