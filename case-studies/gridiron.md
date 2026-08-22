# Gridiron

**Private case study · TypeScript · discord.js · SQLite · live operations**

[Back to profile](../README.md)

## Outcome

Gridiron runs a private sports-league community end to end: scheduling, team ownership, trades, a draft room, free agency, waivers, playoff brackets, and league news. It has run 24/7 since **August 8, 2026**.

Two product decisions shaped everything else.

**It never handles publisher credentials.** Comparable bots reverse-engineer a game publisher's private API or ask members for their game-account logins. Gridiron works entirely without either. The one sync path it supports is the publisher's own export screen, which posts league data to a URL the user types in — no login, no stored credential, and nothing for the publisher to revoke. Choosing the slower integration was the point.

**It is panel-first, not command-first.** Only two slash commands exist; everything else is buttons on pinned, self-refreshing panels. Component identifiers are stateless, encoding the action and its arguments rather than a session, so panels keep working after a restart or a redeploy. A registration test enforces the command ceiling so the design cannot erode by accident.

## What I worked through

- Twelve feature modules, seven background job types, and eighteen database migrations applied at boot.
- An **exact-construction** season scheduler: a double round-robin within divisions plus a circle-method rotation across them, producing a guaranteed 18 weeks, 18 games, 9 home and 9 away for every team — a construction, not a search that might fail.
- Provisioned the community itself programmatically: 12 categories, 63 channels, 21 roles, 77 bound settings.
- Idempotent maintenance scripts that replace their own output instead of stacking duplicates.
- A supervised deploy path with a verified online database backup taken before each release.

## Fresh verification

On **August 11, 2026** the full check gate passed at exit 0 — typecheck, tooling typecheck, and **36 test suites** — with the running build confirmed to have been compiled from current source.

The same pass closed out a defect the project's own notes had recorded as an open blocker: a reported missing import that did not reproduce, because the symbol was imported and exported correctly. Correcting the record mattered as much as the code — a stale blocker costs the next person a day of hunting.

## The test that earned its keep

Message-payload limits are enforced by the platform at runtime, not by the type system. A rendering test that builds every one of 25 real views against a fresh league and asserts the platform's own rules — unique identifiers within a message, row and option ceilings, character caps — found **two crash classes that were already live**:

- Two menus shared a component identifier, which broke team claiming on every newly created league.
- Two navigation buttons collided whenever a user viewed one week ahead of the league's current week.

Both were invisible to typecheck and to unit tests, and both were fixed by making the identifiers distinguishable. Every new view is now added to that test's list.

## Reliability and blast radius

- The data-ingest endpoint bound to every interface, reachable across the local network and the private mesh, for a service that only ever needed loopback. It now binds a configurable address defaulting to **loopback**.
- Raw uploaded payloads accumulated without limit in the same database the bot plays out of. They now age out on a retention window: the payload body is cleared while the audit row survives, so history is preserved without the bulk.
- An unhandled promise rejection used to terminate the process, and the supervisor waits a fixed interval before respawning — one stray background promise cost the whole league a minute of downtime. Those are now logged and survived; genuinely fatal errors still exit.

## What this demonstrates

- Owning a service that real people depend on, including deploys, migrations, backups, and incident behavior.
- Writing tests against the constraints that actually break production, not only the ones a compiler can see.
- Making a deliberate integration trade — slower path, no credential custody — and documenting why.
- Reducing exposure and retaining data on purpose rather than by default.
- Correcting a stale record so the next person does not re-debug a solved problem.

## Boundaries

The source is private and the bot runs in a single private community. **Rate limiting on the ingest endpoint remains an open item** — unauthenticated traffic reaches the database before it is rejected, and it shares that database with gameplay writes. It is listed here because a known gap stated plainly is worth more than an unqualified claim.
