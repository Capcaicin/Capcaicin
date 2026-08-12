# LifeOS

**Private case study · Next.js · TypeScript · Supabase/Postgres · Edge Functions · Docker**

[Back to profile](../README.md)

## Outcome

LifeOS is a private, self-hosted personal-operations system for capturing and reviewing daily activity through web and shortcut workflows. It combines a Next.js application, a shared TypeScript domain package, Supabase/Postgres, and Edge Functions in one documented operating model.

The central product rule is simple: evidence stays visible. Missing data is not rendered as zero, observational patterns are not described as causes, consequential writes are previewed, and automated agents cannot independently send messages, pay, delete records, or change medication.

## What I worked through

- Structured a modular monolith across the web application, shared domain logic, database migrations, and Edge Functions.
- Designed scoped authentication and authorization boundaries, including row-level security, write-limited device flows, revocation, and audit records.
- Built command-first and form-based capture paths, offline-aware behavior, reviews, and a privacy center.
- Added explicit contracts for evidence quality, safety screening, deduplication, recommendations, and null handling.
- Documented architecture, data classification, threat modeling, deployment, backup, recovery, known limitations, and go-live gates.

## Fresh verification

Run against the current local worktree on **August 12, 2026**:

- `npm run verify` passed strict TypeScript checks for both workspaces.
- Vitest passed **20 test files and 416 tests**.
- ESLint completed successfully.
- The optimized Next.js production build completed successfully.
- The source and freshly built browser bundle passed the repository's secret and client/server-boundary scan.

## What this demonstrates

- Translating broad product requirements into enforceable technical rules.
- Working across frontend, backend, database authorization, automation, and operations.
- Treating privacy and failure behavior as product features.
- Using automated checks and written handoffs to make AI-assisted implementation reviewable.

## Boundaries

The source remains private because the product handles personal data and local infrastructure details. The checks above establish the state of the current local worktree; they do not claim that every planned physical-device workflow or later production change has been accepted or deployed.
