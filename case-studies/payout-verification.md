# Game payout verification

**Private case study · Python · Svelte · PixiJS · simulation · release integrity**

[Back to profile](../README.md)

## Outcome

A nine-mode game engine had to prove three things before it could ship: that its long-run return matched the declared figure exactly, that no outcome could exceed the maximum-win ceiling, and that the published lookup tables the platform would actually serve were byte-for-byte the ones that had been verified.

Two halves feed each other. A Python math package generates outcome books and lookup tables through large-scale simulation; a Svelte and PixiJS frontend renders those outcomes. My work was to make the claim about the math independently reproducible rather than trusted, and to keep the verified artifact and the shipped artifact provably identical.

## What I worked through

- Built a verification pass that recomputes each mode's return **from the published lookup tables**, rather than re-reading the generator's own output — so a bug in generation cannot certify itself.
- Ran the full regeneration and verification of all nine modes end to end as a single reproducible job.
- Added format and integrity checks over every published table: SHA-256 plus a payout hash across 100,000 entries per mode.
- Compared the staged submission bundle against the verified build file by file, so "what was tested" and "what would be uploaded" are the same objects.
- Maintained the frontend test suite alongside the math suite, so a rendering change cannot silently break an outcome path.

## Fresh verification

Run on **July 28, 2026**, roughly 23 minutes, exit 0:

- All **9 modes** independently recomputed from the published lookup tables to a return of **0.960000 exact**.
- Maximum win held at **25,000x** with **0 over-cap outcomes**.
- SDK format checks **9/9**, each covering SHA-256 and payout hashes over **100,000 entries**.
- Frontend tests **322/322**; math tests **35/35**.
- Staged bundle rebuilt at 159 files: frontend byte-identical, math restaged **19/19 SHA-identical**.

## The defect worth describing

An early verification pass reported a catastrophic failure: outcomes appeared to blow through the maximum-win ceiling by orders of magnitude. Nothing was wrong with the data.

Two assumptions were wrong at once. Payout values are expressed in hundredths in both the outcome books and the lookup tables, and the maximum win is a multiple of the **base** bet rather than each mode's own entry cost — so a mode costing 200x the base bet legitimately tops out at 125x its own price. A naive verifier that reads the units at face value and normalises against the wrong baseline reports a disaster that does not exist.

Finding that meant reading the platform's format spec against the generator's output instead of trusting either in isolation. It is the reason the verification pass now states its unit and baseline assumptions explicitly at the top of its output — a false alarm that costs a day is still a defect, just in the test rather than the system.

A second recurring class of bug came from a padded rendering grid: the display board carries a padding row at each end, while the game's logical coordinate space does not. Code that walked the padded length while indexing the unpadded space left undefined slots that the renderer then dereferenced. Boundary mismatches between two representations of the same board accounted for more debugging time than the math ever did.

## What this demonstrates

- Designing verification that is independent of the thing it verifies.
- Large-scale simulation and statistical validation against an exact declared target.
- Release integrity: hashing published artifacts and proving the tested build is the shipped build.
- Diagnosing a false failure by questioning the test's assumptions rather than patching the system.
- Holding a release at a human gate when the remaining risk is judgement, not code.

## Boundaries

The source and the platform relationship remain private, and the game has **not** been submitted — visual review and upload are deliberate human gates that had not been cleared as of the verification date. The figures above describe the verified staged build; they are not a claim of acceptance, approval, or release by any third party.
