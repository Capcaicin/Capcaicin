# RareLink

**Private case study · Next.js 15 · React 19 · Supabase/Postgres · Stripe Connect**

[Back to profile](../README.md)

## Outcome

RareLink is a collectibles marketplace built around a **protected checkout**: a buyer's funds are held against a specific order rather than released to a seller at the moment of payment, so the platform can stand between the two parties while an item is in transit.

That single product requirement is what makes it a payments problem rather than a shopping-cart problem. It is implemented on Stripe Connect using **separate charges and transfers** — the platform takes the charge, then moves funds to the seller as a distinct, later, individually auditable operation. Destination charges would have been less code and the wrong shape.

## What I worked through

- A Next.js 15 and React 19 application with a Supabase/Postgres data layer, transactional email, and a component system on Tailwind and shadcn/ui.
- Authorization enforced in the database through row-level security, so a missed check in application code does not become a data leak.
- Marketplace surfaces across listings, orders, collections, and administration — 39+ routes.
- A pricing subsystem with its own invariants, aggregation, and history.
- A reproducible way to expose a local build over a public URL for review, after an earlier tool put an interstitial page in front of every visitor.

## Fresh verification

On **May 23, 2026**:

- **39+ routes** building.
- `tsc --noEmit` at exit 0 under strict settings.
- **0 npm audit vulnerabilities**.

## The defect worth describing

A pricing query needed an index on a time-bucketed expression. Postgres rejected it — the truncation function is not immutable when applied to a timestamp with time zone, because its result depends on the session's time zone setting, and an index cannot be built on an expression whose value can change underneath it.

The tempting fix is to mark the expression immutable and move on, which produces an index that is silently wrong for any session in a different time zone. The correct fix is to make the value deterministic before it is indexed. That distinction — between an error the database is raising for a good reason and an obstacle to route around — is the part I would want to be judged on.

A second, more ordinary trap: server-only module guards protect the pricing code from ever reaching the browser, and also block the scripts that need to exercise it offline. That is solved with an explicit shim at script startup, not by weakening the guard.

## What this demonstrates

- Implementing a payments flow whose shape is driven by a trust requirement, not by convenience.
- Enforcing authorization at the data layer rather than only in application code.
- Reading a database's refusal as information about correctness.
- Keeping a security boundary intact while still making the code testable.

## Boundaries

The source is private. The application runs locally and is exposed for review through a temporary tunnel; there is **no production deployment and no live money rail**. Stripe integration is implemented and exercised in test mode — this is not a claim of processed real-world transactions, settled payouts, or dispute handling at volume.
