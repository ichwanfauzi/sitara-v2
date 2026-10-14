# Architecture Decision Records (initial)

## ADR-001: Modular monolith

**Decision:** Start with one FastAPI backend and one React frontend, structured into modules.

**Reason:** Fits a solo developer, reduces deployment complexity, and preserves clear boundaries without premature microservices.

## ADR-002: PostgreSQL

**Decision:** Use PostgreSQL for relational business data and transactional consistency.

**Reason:** SITARA has connected records, access controls, workflow transitions, and audit history.

## ADR-003: One notetaker writes during a live meeting

**Decision:** During a live meeting, only the designated notetaker may edit meeting notes; authorized leaders/viewers are read-only.

**Reason:** Matches the specified workflow and reduces concurrent-edit conflicts in the first release.

## ADR-004: Official status is controlled by Secretariat

**Decision:** Only authorized Secretariat users may change an action item's official status. PIC and leaders submit progress updates; they do not directly change the official status.

**Reason:** Establishes a single accountable workflow for official monitoring status. This must be enforced server-side and tested.
