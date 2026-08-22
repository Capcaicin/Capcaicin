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

## Update — August 20, 2026: drift control and restorable backups

Two additions since the verification above, both aimed at the same problem: documentation that quietly stops being true.

**A verifier that binds prose to reality.** Ten checks now run against the live system rather than against the repository's own description of itself. Every count written in the documentation must equal the live local count or the production count on record; commit hashes must resolve; a section that calls itself complete may not hold an unchecked box; the private-network layer must be serving exactly the recorded listeners with public exposure off; the newest backup generation must still have a verified remote twin.

Its most important property is that **unavailable is not success**. When a probe cannot reach what it needs to check, the verifier exits *inconclusive* — never *pass*. A self-test proves all ten probes still detect the drift they were written to catch, so the verifier cannot rot into ten functions that always return true. It runs as a separate operational tier, deliberately outside the commit gate, because one of its checks can only be satisfied by a rebuild that disturbs the running service — and a gate people learn to bypass is worse than no gate.

**Backups with the restore path exercised.** The newest database generation is held as symmetrically encrypted ciphertext on a separate always-on machine, reachable only over the private mesh, and the decrypt path has been run **from the remote copy alone** rather than assumed. Two limits are recorded alongside the claim rather than omitted from it: that machine is on the same local network, so this is machine-loss recovery and not site-loss recovery; and recovery requires a passphrase whose authoritative copy belongs in a password manager, not on the host. Shipping is idempotent by generation identity rather than by hash, because symmetric encryption is salted and identical input produces different bytes on every run.

Custody remains manual until a scheduled task is registered, and the verifier fails on staleness in the meantime. That is the intended behavior: a backup nobody confirmed is a backup nobody has.

## What this demonstrates

- Translating broad product requirements into enforceable technical rules.
- Building verification that reports uncertainty honestly instead of defaulting to green.
- Working across frontend, backend, database authorization, automation, and operations.
- Treating privacy and failure behavior as product features.
- Using automated checks and written handoffs to make AI-assisted implementation reviewable.

## Boundaries

The source remains private because the product handles personal data and local infrastructure details. The checks above establish the state of the current local worktree; they do not claim that every planned physical-device workflow or later production change has been accepted or deployed.
