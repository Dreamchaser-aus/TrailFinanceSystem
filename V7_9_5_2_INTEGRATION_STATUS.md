# BankFlow V7.9.5.2 – UTC Closing Integration (development only)

## Implemented
- `/closing` requires a verified per-bank UTC anchor, calculates the next scheduled boundary and stores a `ClosingPeriod` linked to the Closing record atomically.
- UTC continuity uses prior `ClosingPeriod.end_utc` as next `start_utc`; boundary interval is [start,end).
- Existing historical Closing rows are not guessed or rewritten. Banks with historical Closing rows cannot be initialized via the simple form; they need a separately verified historical migration.
- Existing closed UTC periods block ordinary edit/void operations for transactions recorded within them.
- Admin can initialize a boundary only for a bank with no historical closings. Audit trail records initialization and closing.
- Old date-based same-day closing guard remains in place to prevent unintended duplicate entries.

## Not ready for production
- Dashboard, Active Bank Balances, Transaction Management and Daily Reconciliation report queries still use business_date and are NOT converted to UTC periods.
- The system balance displayed on closing is a current ledger balance, not a period-specific snapshot; financial reconciliation is NOT validated.
- Transactions currently use created_at rather than a separately verified occurred_at timestamp. Backdated entries need explicit policy.
- Initial anchor for banks with historical closing requires a manual reconciliation/migration workflow.
- PostgreSQL integration, concurrency, idempotency and end-to-end DST tests have NOT been executed.
- Changing closing policy while a period is open requires a business decision and stronger effective-dated policy history.

DO NOT deploy this development build to production.
