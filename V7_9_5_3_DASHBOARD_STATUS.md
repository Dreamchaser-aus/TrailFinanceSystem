# Dashboard UTC integration (testing build)

Implemented: Dashboard date-range to UTC half-open closing boundaries; confirmed bank ledger Opening/IN/OUT/Closing from period_reporting; transaction KPI, latest, customer activity and dealer totals filtered on the same UTC window. Existing Unclaimed is current-status based and NOT historically reconstructable. Bank status reconstruction and closed-bank list remain legacy date-based. Historical periods are not pinned to stored ClosingPeriod policy snapshots when the admin changes closing time. PostgreSQL concurrency/idempotency and Railway staging tests have NOT been performed. Do not deploy to production.

Run: python -m unittest discover -v
