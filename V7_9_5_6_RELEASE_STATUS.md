# BankFlow V7.9.5.6 — Release Candidate (Staging)

## Changes
- PostgreSQL BEFORE UPDATE/DELETE triggers prevent changes to Closing, ClosingPeriod and ClosingFinancialSnapshot. Installed transactionally at every bootstrap; startup fails if guard creation fails.
- Unclaimed claim now takes the bank lock BEFORE the lead row lock, matching Closing lock ordering. This serializes claim and closing snapshot for the same bank.
- Existing unique constraints and indexes remain in place for closing period, snapshot, and transaction linkage.
- Root test module renamed to remove pytest duplicate module name collision.
- Added PostgreSQL-specific isolated concurrency/immutability verification script.

## Limitations (not production-approved)
- The Unclaimed snapshot is observed at Closing execution, not reconstructed as-of end_utc.
- Database triggers prevent UPDATE/DELETE, but a privileged DB owner can remove them; access control and backups remain necessary.
- Existing historical Closing rows are not automatically migrated or retroactively snapshotted.
- PostgreSQL concurrency test requires an explicitly supplied disposable test DATABASE URL; never run against production.
- End-to-end Railway restart and live application concurrency remain user staging acceptance tasks.
- A repeat submission may still display a validation error rather than return an idempotent success; uniqueness protects stored records.
