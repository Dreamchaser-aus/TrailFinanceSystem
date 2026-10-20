# BankFlow V7.9.5.3 — Partial UTC Financial Integration (NOT FINAL)

This is a complete source-tree ZIP for development review, NOT a production-ready final build.

Implemented in this iteration:
- UTC-only per-bank ledger report engine (`period_reporting.py`), half-open boundaries and Decimal balances.
- Closing system balance now computed as of period end, excluding transactions after end.
- New `/reports/utc-reconciliation` report with Opening/IN/OUT/Closing arithmetic.
- UTC boundary tests for Melbourne DST 23/25 hours and continuity.
- Source compilation succeeds; 6 algorithm unit tests pass.

NOT COMPLETE / NOT VERIFIED:
- Existing Dashboard, Active Bank Balances and transaction-management date reports still have legacy business_date calculations; they are NOT unified.
- Reconciliation route uses current policy to calculate historical reporting boundaries; effective-dated policy snapshots are not implemented.
- Historical opening balances and claimed/unclaimed state history need stronger audit rules.
- PostgreSQL integration, unique-reference collision, simultaneous closing/transaction concurrency, idempotency, end-to-end UI tests are NOT run.
- Flask and database dependencies are not installed in this execution environment; application import/runtime checks could not run.
- Do not deploy to an existing Railway environment containing valuable data.

To proceed: run with a new Railway staging PostgreSQL database and perform full integration tests before finalizing V7.9.5.3.
