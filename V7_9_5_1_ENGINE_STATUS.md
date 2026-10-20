# BankFlow V7.9.5.1 — Closing engine implementation (NOT production-ready)

Implemented:
- closing_engine.py: timezone-aware next closing UTC boundary, DST fold/gap handling, left-closed right-open transaction membership, continuity check.
- ClosingPolicy and ClosingPeriod database models (new tables on bootstrap; no automatic backfill of legacy Closing records).
- Admin Business Timezone Active/Inactive + manual GMT + closing wall clock settings, with Audit record.
- Four unit tests for 23/25-hour transitions, manual GMT, and boundary exclusivity.

NOT implemented / NOT verified:
- Closing POST still uses the legacy Closing model and does not write ClosingPeriod.
- Dashboard, Daily Reconciliation, Transaction Management, Active Bank Balances, Unclaimed and balance history still use legacy business_date logic in places.
- No migration of historical Closing rows; real historical boundaries cannot be inferred from business_date.
- No PostgreSQL integration or concurrency/locking tests.
- This package must not replace the production Railway deployment.

Run local automated unit tests in an isolated environment:
  python -m unittest discover -s tests -v

The next development step is to explicitly seed a verified closing boundary per bank, then atomically record ClosingPeriod on close and migrate ALL report queries to period UTC ranges, including deletion/void controls and snapshots.
