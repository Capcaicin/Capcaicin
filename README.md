# Capcaicin

### AI-assisted technical implementation · QA · automation · support-minded engineering

I turn ambiguous requirements into scoped, testable systems and stay with the work through debugging, documentation, and handoff. I care about the part after a demo works: permissions, failure paths, privacy, reproducible checks, and an honest statement of what is still unproven.

I use AI tools openly as part of development. I remain accountable for requirements, technical decisions, integration, testing, and the accuracy of the claims I publish. Every number on this page comes from a check I can re-run.

**[LinkedIn](https://www.linkedin.com/in/timothyannorino/)** · Orlando / Lake Mary, FL · open to remote

## Where I fit

I am building toward roles where technical fluency and clear communication matter together:

- Technical Implementation Specialist
- QA / Software Tester
- AI Operations or AI Application Evaluator
- Technical Support Engineer
- Customer Success Engineer

Before software I spent four years turning messy operational processes into documented ones: event delivery and escalation at Topgolf, then CRM workflow ownership, dialer provisioning, and the internal training wiki for 30+ onboarded agents at an insurance agency. The instinct is the same — take the thing only one person knows how to do, and make it repeatable.

## Selected case studies

These projects are private because they contain personal, operational, or pre-release material. The linked case studies explain the work without exposing source code, credentials, customer data, or personal records.

| Project | What I built and validated | Current evidence | Status |
|---|---|---|---|
| [LifeOS](case-studies/lifeos.md) | A private Next.js and Supabase personal-operations system with command-first capture, scoped access, evidence-based insights, and self-hosted operations. | On August 12, 2026: strict TypeScript checks, 416 automated tests, lint, a production build, and a built-browser secret-boundary scan all passed. A 10-check drift verifier added August 20 binds written claims to live system state and returns *inconclusive* rather than *pass* when it cannot prove one. | Private source; local changes verified; physical-device and later production gates remain explicit. |
| [Game payout verification](case-studies/payout-verification.md) | Independent verification of a 9-mode game engine's payout model — return-to-player, maximum-win ceiling, and the integrity of every published lookup table. | On July 28, 2026: all 9 modes independently recomputed from the published tables to a return of **0.960000 exact**, with a 25,000x cap and **0 over-cap outcomes**; SDK format checks 9/9 with SHA-256 and payout hashes over 100,000 entries each; **322/322 frontend and 35/35 math tests** green. | Verified and staged; not submitted. Visual review and upload remain human gates. |
| [Gridiron](case-studies/gridiron.md) | A live Discord league-operations bot: stateless button panels that survive restarts, an exact-construction season scheduler, and a deliberate rule never to handle a user's game-publisher credentials. | Running 24/7 since August 8, 2026. On August 11: full check gate green (typecheck, tool typecheck, **36 test suites**) across 12 modules and 18 migrations. A runtime-limits test I added caught **two live crash classes** static analysis could not see. | Live in one private server. Rate limiting on the ingest endpoint is a known open item, documented rather than hidden. |
| [Vault RAG](case-studies/vault-rag.md) | A dependency-free passage-retrieval engine over a private knowledge base, exposed to AI clients as a tool, with health monitoring designed so silence is the alert. | On August 22, 2026: 589 curated notes indexed as **6,215 passages / 1.2M tokens**, full rebuild in **80 seconds for $0.023**, incremental re-index by content hash. Health is emitted as structured JSON and pushed as a heartbeat carrying *measured* health, not exit status. | Private local system; running nightly as a non-blocking stage. |
| [OpenClaw](case-studies/openclaw.md) | An Obsidian-based knowledge-operations system with a project registry, bounded MCP context compiler, automated health views, and provenance-aware handoffs. | On August 12, 2026: 5/5 context-compiler tests passed; the vault audit reported 513 curated notes with zero broken curated links, orphans, empty notes, or missing frontmatter. | Private local system; audit results measure structure, not the truth of every note. |
| [RareLink](case-studies/rarelink.md) | A protected-checkout marketplace on Next.js 15 and React 19 with Supabase row-level security and Stripe Connect using separate charges and transfers. | On May 23, 2026: **39+ routes**, a clean `tsc --noEmit`, and **0 npm audit vulnerabilities**. Pricing work included a Postgres index defect traced to a non-immutable expression. | Private source; runs locally behind a tunnel. No live money rail and no production deployment claim. |
| [CustomDesk](case-studies/customdesk.md) | A local custom-order operations prototype with deterministic pricing, workflow replay, accessibility checks, and separate human-approval gates. | On August 12, 2026: the complete 16-stage local verifier passed, including 618 deterministic replay checks and focused privacy, accessibility, HTTP-boundary, and tamper controls. | Phase 0 only; no customer-validation, payment, or public-deployment claim. |

## Practices, and the artifact that proves each

| Practice | Where it is demonstrated |
|---|---|
| Regression testing that finds real defects | A runtime payload-limits test in Gridiron caught two crash classes already shipping in production |
| Verification that fails honestly | LifeOS's drift verifier exits *inconclusive*, never *pass*, when a probe cannot run — and self-tests that all 10 probes still catch their own drift |
| Deterministic replay | CustomDesk re-runs 618 recorded cases on every change |
| Data integrity at scale | SHA-256 and payout hashes across 100,000-entry lookup tables, recomputed per release |
| Reducing blast radius | Narrowed a service from all-interfaces to loopback; added retention pruning so raw payloads age out while the audit trail survives |
| Backups you have actually restored | Encrypted off-machine custody with the decrypt path exercised from the remote copy alone — and the limits of that guarantee written down |
| Debugging past a false alarm | A payout verifier reported catastrophic failure until I traced it to unit and baseline assumptions rather than the data |
| Cost and performance measurement | Retrieval index rebuild reported in seconds and cents, not adjectives |

## How I work

1. Clarify the outcome, constraints, and actions that require human approval.
2. Build the smallest useful path and keep private data out of public surfaces.
3. Test normal behavior, failure behavior, permissions, accessibility, and secret handling.
4. Document what passed, what remains gated, and how another person can continue the work.

## Working stack

- **Languages** — TypeScript, JavaScript, Python, SQL, PowerShell, Bash
- **Web** — Next.js, React, Node.js, Svelte, Tailwind, shadcn/ui
- **Data** — Postgres, Supabase (including row-level security and self-hosting), SQLite
- **Platform** — Docker, Linux, GitHub Actions, Cloudflare Tunnel, Tailscale, Raspberry Pi / ARM
- **Integrations** — Stripe Connect, Discord API, Resend, OpenRouter, Model Context Protocol, embeddings and retrieval
- **Practice** — Vitest, pytest, typecheck and lint gates, secret-boundary scanning, accessibility checks, uptime monitoring, encrypted backup and restore drills

Currently studying for **CCNA 200-301** and **CompTIA Security+ SY0-701**.

## A note on authorship

AI-assisted development is part of my workflow, not a hidden footnote. I use coding agents to accelerate research and implementation, then inspect the result, run repeatable checks, debug failures, and document limitations before treating the work as complete.
