# BankFlow V7.9.6.0 — Stable Release Package

Release source: BankFlow V7.9.5.6 Release Candidate (the user's accepted Railway staging baseline).

## Packaging changes
- Version label set to 7.9.6.0 (VERSION file).
- Core financial calculations, application routes, database schema, and safeguards are unchanged from V7.9.5.6.
- Removed generated Python caches and pytest cache from distribution.
- Includes all Flask source files, templates, migration scripts, test scripts, and Railway deployment configuration.

## Known limitations carried forward
- Historical Unclaimed snapshot captures the state at the time Closing executes; it does not reconstruct arbitrary earlier end_utc states.
- Historical Closing records are not retroactively migrated or backfilled.
- Database triggers prevent UPDATE/DELETE on protected snapshots, but privileged database owners can alter database protections.
- Concurrent duplicate requests may return a validation error instead of an idempotent success response.

## Validation and deployment
- User reports V7.9.5.6 Railway staging testing succeeded. This is user-reported acceptance, not independently reproduced production testing.
- Use a separate database and backup before production deployment. Avoid resetting any existing database unless explicitly intended.
- Run automated tests and staging PostgreSQL concurrency script with disposable test credentials before deployment.
