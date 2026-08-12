# OpenClaw

**Private case study · Obsidian · Model Context Protocol · Node.js · knowledge operations**

[Back to profile](../README.md)

## Outcome

OpenClaw is a private knowledge-operations system built around an Obsidian vault. Its purpose is to preserve project history without forcing each new AI session to ingest an entire archive or trust a stale summary.

The system treats fresh repository and runtime evidence as stronger than historical notes. It routes a task through a project registry, compiles bounded context for the requested intent, carries forward blockers and human-approval gates, and keeps raw session exports separate from curated project truth.

## What I worked through

- Established a canonical vault structure for projects, decisions, learning, sessions, and system operations.
- Built a registry that resolves project names and aliases to the correct source-of-truth notes.
- Added an MCP context compiler with explicit build, diagnose, plan, research, and reflect intents.
- Generated compact working-memory and health views for fast orientation.
- Added provenance, freshness, redaction, projection-consistency, and handoff rules.
- Automated link, orphan, empty-note, and frontmatter checks across the curated graph.

## Fresh verification

Run against the private local system on **August 12, 2026**:

- The context compiler passed **5/5 automated tests**.
- The vault audit counted **1,028 Markdown notes**, including **513 curated notes**.
- The curated graph had **0 broken links, 0 orphans, 0 empty or near-empty notes, and 0 notes without frontmatter**.

## What this demonstrates

- Designing AI workflows that retrieve bounded, task-relevant context instead of dumping history into every prompt.
- Maintaining durable project state, provenance, and handoffs across tools and sessions.
- Distinguishing current evidence from generated projections and old notes.
- Building automation around a human-readable knowledge base without making the automation the sole source of truth.

## Boundaries

The vault and its source material remain private. The audit measures graph structure and hygiene; it does not prove that every statement in every note is current. Project-specific runtime, deployment, and approval claims are rechecked at the source before they are presented as current.
