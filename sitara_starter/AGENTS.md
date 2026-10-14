# Instructions for AI coding agents working on SITARA

## Non-negotiable rules

1. Read the relevant README, ADRs, test strategy, and acceptance criteria before editing.
2. Use TDD: add a meaningful test first, run it to confirm the expected failure, implement the smallest correct change, then run focused and regression tests.
3. Never weaken, delete, skip, or rewrite an assertion merely to make a failing test pass. Explain any test change that changes intended behavior.
4. Never add real credentials, tokens, private keys, production URLs containing secrets, or confidential meeting data to source, fixtures, screenshots, prompts, logs, or docs. Use `.env.example` placeholders and synthetic fixtures only.
5. Do not disable or bypass Gitleaks, Semgrep, `npm audit`, `pip-audit`, lint, type checks, or CI gates to make a build green. Report findings and propose a fix.
6. Do not connect to or run destructive tests against production. Database changes must use versioned Alembic migrations.
7. Do not claim a command or test passed unless it was actually executed and its result observed. Clearly state tests that could not be run.
8. Keep changes small and layered. Do not introduce a design pattern, dependency, or abstraction without a concrete need.

## SITARA domain rules

- Roles are distinct: `SUPER_ADMIN`, `SEKRETARIAT`, `REKTOR`, `WAREK`, and `PIC`.
- Super Admin is not the same account/operational role as Sekretariat.
- Full minutes and restricted Decision Briefs are accessible only to authorized leadership and Secretariat accounts. PIC users must not obtain them through direct URLs, API IDs, search, exports, or document-storage URLs.
- During a live meeting, only the designated notetaker can edit meeting minutes; authorized viewers are read-only.
- Official task status is controlled by authorized Secretariat users. PIC and leadership submit progress; they do not directly mutate the official status.
- The five official task statuses are `BELUM_DIMULAI`, `BERPROSES`, `TERKENDALA`, `MENUNGGU_ACC`, and `SELESAI`.
- A `SELESAI` state requires the required verification/approval record and must be represented consistently in audit history.
- A decision may or may not become an action item. Do not create a task silently when `is_action_item` is false.
- A task can have one active main PIC and one or more supporting PICs. Validate delegations against the user's authorized organizational scope.
- Document content is private by default. Do not return raw storage keys or permanent public URLs to unauthorized users.
- Audit important actions server-side, including permission changes, status transitions, approvals, exports of restricted data, and Super Admin actions. Do not log secrets or entire confidential documents.

## Before submitting a change

- Run relevant backend tests, Ruff, formatting, and mypy.
- Run relevant frontend tests, lint, format check, type/build checks, and dependency audit.
- Add negative authorization tests for security-sensitive routes.
- Check the diff for secrets and unintended files.
- Update docs/ADRs when behavior or architecture changes.
- Provide a concise summary, tests actually run, results, and known limitations.
