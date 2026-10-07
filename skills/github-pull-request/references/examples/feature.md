# Example — feature PR (UI + API + migration + permissions)

A fictional project. Every optional section appears here because this branch triggered all of
them — a smaller PR must not copy sections whose trigger did not fire (see `../pr-body-template.md` §2).

Title: `feat(billing): invoices can be voided and restored`
(base `dev` ← head `feature/invoice-void`)

```markdown
## Summary
Invoices could only be created and paid. Finance staff can now void an unpaid invoice and restore
it later; voiding no longer leaves reminder emails and payment links active.

## Feature details

### 1. Void an invoice
- **Who:** `billing.manage` (seed: Finance, Admin), limited to invoices of the user's own company.
- **How:** "Void" in the row menu of the Invoices table → confirm dialog.
- **Behavior:**
  - Only `DRAFT` or `SENT` invoices can be voided; `PAID` invoices show the action disabled with a tooltip.
  - In one transaction: status → `VOID`, `voided_at` / `voided_by` recorded, pending reminder jobs cancelled, the payment link revoked.
  - Double submit (two tabs) → the second request gets "Invoice is already void." and the list refreshes.
- **Messages:** "Invoice is already void." · "Paid invoices cannot be voided — issue a credit note instead."
- **API:** `POST /api/v1/invoices/{id}/void/`

### 2. Restore a voided invoice
- **Who:** `billing.manage` at the invoice's company; outside scope → 404 (existence not revealed).
- **How:** "Voided" filter → "Restore" on the row.
- **Behavior:** status returns to what it was before voiding; a new payment link is issued; reminders are re-scheduled from today, not from the original due date.
- **API:** `POST /api/v1/invoices/{id}/restore/`

### Removed / behavior changes
- `DELETE /api/v1/invoices/{id}/` is removed — use void.
- `status` is now read-only in `PATCH`; changing it returns 400.

## Docs
- Spec: `docs/specs/2026-03-02-invoice-void.md` (D-1…D-7)

## Migrations & deployment
- `billing/0012_invoice_void_audit` — adds `voided_at`, `voided_by`, `status_before_void` (reversible)
- ⚠ After deploy, run `manage.py cancel_orphan_reminders` once to clear reminders of invoices deleted before this release.
- New environment variables: none.

## Permissions
- No new codes: `billing.view` (list, filter), `billing.manage` (void, restore) at the invoice's company.
- Row actions are hidden exactly when the API would refuse them.

## Testing
- Backend: `pytest billing -q` — 214 passed
- Frontend: `tsc` / `eslint` / `vitest` — pass
- E2E: `e2e/invoices-void.spec.ts` 6/6

## Known limitations / follow-ups
- No bulk void yet.
- Voided invoices are still counted in the monthly export (fix planned in D-6).

## Review checklist
- [ ] Matches the spec / issue, no scope creep
- [ ] Access checks enforced server-side; hidden in UI ⇔ blocked by the API
- [ ] Migrations run cleanly forward (and backward if reversible); deploy notes complete
- [ ] New/changed user-facing text reviewed
```
