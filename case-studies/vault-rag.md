# Vault RAG

**Private case study · Node.js · embeddings · retrieval · monitoring**

[Back to profile](../README.md)

## Outcome

A knowledge base of several hundred long-form notes was already searchable, but only as whole documents — a 40 KB note was one opaque unit, so a question about one paragraph returned the entire file and burned context on the other 39 KB.

Vault RAG indexes the same material passage by passage and exposes it to AI clients as a tool. It has **zero external dependencies**: the engine, the CLI, and the credential resolution are plain Node, and the only thing it needs beyond the filesystem is an embeddings endpoint.

The harder design question was not retrieval quality but **which retrieval surface a question should reach at all**. Three now exist — current state of a known project, historical session memory, and passage search across curated notes — and choosing the wrong one is the primary failure mode. That distinction is documented as the first thing a caller reads, because a fast answer from the wrong index is worse than a slow one from the right index.

## What I worked through

- Chunked and embedded a curated subset of the corpus, deliberately excluding raw session transcripts as noise while keeping one explicitly curated exception.
- Made indexing **incremental by content hash**, so a routine pass re-embeds only what changed.
- Gave each embedding provider its own isolated store, so switching providers cannot silently corrupt an index with mismatched dimensions.
- Exposed the engine as tools on an existing Model Context Protocol server rather than standing up a second service.
- Wrote the integration contract as structured JSON output, so any consumer can render health without parsing prose.

## Fresh verification

On **August 22, 2026**:

- **589 curated notes** indexed as **6,215 passages / 1.2M tokens**.
- Full rebuild: **80 seconds, $0.023**. Incremental passes are seconds and fractions of a cent.
- Runs nightly as a **deliberately non-required stage** — a network hiccup in a nice-to-have index must not fail the whole nightly chain.

## Two findings worth keeping

**Environment is not where a credential lives.** Tool hosts spawn a server through a transport that hands it a filtered environment, and the OS scheduler runs tasks with no user environment at all. A key read only from `process.env` works perfectly when a developer runs it by hand and fails silently in both places it actually needs to run. Credential resolution now falls back through environment, then a local file, then an existing authentication profile. The general rule — never write environment-only credential lookup for anything a host or a scheduler will launch — now applies to everything in the project.

**Verify the vendor claim before designing around it.** The widely repeated belief that the provider in use serves only chat completions is wrong; its embeddings endpoint returns correct 1536-dimension vectors. Confirming that with one request avoided routing an entire subsystem through a second vendor for no reason.

## Monitoring: silence is the alert

This is a nightly batch job, not a service you can poll — nothing answers a health check between runs, so an ordinary uptime monitor would either be permanently red or meaningless.

Instead, a completed index **pushes a heartbeat**, and the absence of a heartbeat is the alarm. The important detail is what the heartbeat carries: not the job's exit status, but **measured** health — that the vector and passage counts still align, that the store is non-empty, that the newest content is under a freshness threshold, and that the backlog of unindexed notes is under a ceiling. A job can exit 0 and still have produced a broken index, so exit status was never the right signal.

A desktop status indicator was built first as a standalone tray application, then **backed out** rather than kept — it duplicated a surface that already existed, and a second thing to maintain is a cost even when it works. The integration contract survived; the redundant client did not.

## What this demonstrates

- Building retrieval as an engineering system: chunking, incremental indexing, provider isolation, measured cost.
- Designing monitoring around the failure you actually have, rather than the one a template assumes.
- Debugging an environment-dependent failure that only appears under a host or a scheduler.
- Checking a widely repeated assumption directly instead of architecting around it.
- Removing something that works when it is not worth its maintenance.

## Boundaries

The knowledge base and its contents are private. The figures above describe index structure, cost, and freshness — they measure that retrieval is healthy and current, not that any individual note is factually correct.
