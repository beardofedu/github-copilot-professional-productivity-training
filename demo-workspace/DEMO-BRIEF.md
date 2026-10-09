# Weekly Account Health Report

Build a repeatable workflow that reconciles CRM accounts with product usage and the prior week's results.

## Inputs

- `data/crm_accounts.csv` is the source of truth for account identity, ownership, region, and renewal date.
- `data/product_usage.csv` contains current usage. Its `account_key` may be a CRM account ID or an approved alias.
- `data/prior_week.csv` contains last week's active-user count and risk level.
- `data/account_aliases.json` is the only approved fallback for resolving a non-CRM usage key.

## Required outputs

- `output/reconciled_accounts.csv`
- `output/exceptions.csv`
- `output/weekly-account-health.md`

## Rules

- Never modify files under `data/`.
- Match usage by exact account ID first, then by the approved alias map.
- Never guess an account match.
- Adoption percentage is `active_users / licensed_users * 100`.
- If licensed users are zero, adoption is unavailable and the record requires review.
- Week-over-week change is current active users minus prior active users.
- Flag an account when any of these are true:
  - owner email is blank,
  - adoption is below 40%,
  - last activity is more than 30 days before the report date,
  - renewal is within 90 days,
  - or reconciliation is incomplete.
- Use `2026-10-09` as the report date so the demo is deterministic.

## Quality expectations

- Unmatched and invalid records must remain visible in `exceptions.csv`.
- The Markdown report must distinguish facts, rule-based flags, and unresolved exceptions.
- Add automated tests for high-consequence reconciliation and calculation behavior.
- Use standard Python only.

