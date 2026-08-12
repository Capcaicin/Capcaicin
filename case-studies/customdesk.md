# CustomDesk

**Private case study · deterministic workflows · accessibility · privacy boundaries · evidence tooling**

[Back to profile](../README.md)

## Outcome

CustomDesk is a local Phase 0 prototype for custom-order operations. It explores how an ambiguous service request can move through clarification, pricing, capacity, consent, production, delivery, retention, and redaction without letting an AI system make final commercial or safety decisions.

The governing rule is: **AI interprets. Rules decide. Humans approve.**

## What I worked through

- Built a responsive local landing page and pricing calculator with dark, light, and discreet display modes.
- Created deterministic pricing and lifecycle replay across normal, ambiguous, declined, expired, capacity-constrained, and redaction scenarios.
- Separated private benchmark review, fieldwork preparation, and later manual-send authorization from the public surface.
- Added fail-closed provenance, tamper, privacy, route, storage, and public/private-boundary checks.
- Tested accessible names, contrast, keyboard focus, minimum-width reflow, and real browser behavior.
- Kept synthetic mechanics evidence separate from customer evidence and human approval.

## Fresh verification

Run against the private repository on **August 12, 2026**:

- The complete local verifier passed **16/16 stages**.
- Deterministic workflow replay passed **618 checks across 20 pricing cases and 20 scenarios**.
- The static public surface passed **155 checks**; the exact loopback HTTP boundary passed **22/22** route and policy checks.
- The security-boundary scan passed **15 checks with zero findings**.
- The private fieldwork console passed **210 checks** and the benchmark review workstation passed **74 checks**.
- The durable-state verifier passed **49/49 checks**.

## What this demonstrates

- Turning policy, safety, and operational requirements into executable checks.
- Testing failure paths and tamper cases rather than validating only the happy path.
- Building accessible interfaces while preserving strict public/private boundaries.
- Reporting uncertainty honestly when real customer or human-review evidence is absent.

## Boundaries

CustomDesk remains in Phase 0. The current evidence is synthetic and local: it does not establish customer demand, willingness to pay, provider approval, payment processing, a production security posture, or a public deployment. No outreach or customer messaging is performed by the tooling.
