# booking-v3 date hint tells day-first tenants to type month-first

## Summary
Support ticket #4471 contains **33 unique reports** for a second bug that is distinct from the shared parser issue. On `booking-v3`, the form shows `MM/DD/YYYY` to day-first tenants, so people type month-first while the tenant still expects day-first dates.

## Why this is a separate ticket
- Covers **33 of 412** unique reports merged into #4471.
- Affects **3 tenants**.
- Seen from **2026-04-17** through **2026-09-22**.
- Shows up only in the **form channel (33)**.
- Limited to the `booking-v3` tenants `alder.physio`, `copper.studio`, and `pale.harbour`.

## Example reports
- **R-41230** (`copper.studio`, form): “My client came on 1 June instead of 6 January.”
- **R-41241** (`alder.physio`, form): “We had two people show up on 8 June. They were booked for 6 August.”
- **R-41251** (`pale.harbour`, form): “Wednesday 7 January showed as Wednesday 1 July.”

## Affected tenants
- `alder.physio` (12)
- `copper.studio` (11)
- `pale.harbour` (10)

## Notes
- Intake tags are noisy here too: **15** hint reports were tagged `parser`.
- This issue is separate from the shared parser bug because it is limited to `booking-v3` form entry, not app/email rendering.
