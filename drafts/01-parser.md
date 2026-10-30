# Date parser reads day-first tenant dates as month-first

## Summary
Support ticket #4471 contains **379 unique reports** for one underlying parser bug. The shared parser reads dates month-first even for day-first tenants, so bookings like `7 April` become `4 July`.

## Why this is a separate ticket
- Covers **379 of 412** unique reports merged into #4471.
- Affects **11 tenants**.
- Seen from **2026-04-01** through **2026-10-04**.
- Shows up across **app (204)**, **email (150)**, and **form (25)** reports.

## Example reports
- **R-41200** (`harbour.dental`, app): “Our 7 April reminder went out on 4 July.”
- **R-41202** (`kettle.books`, email): “Invite says Tuesday 12 May. Calendar says Monday 11 May.”
- **R-41203** (`lantern.row`, app): “Booked for 2 December. The invite says 12 February.”

## Affected tenants
- `harbour.dental` (52)
- `kettle.books` (47)
- `nine.lanterns` (44)
- `morrow.tax` (40)
- `long.table` (39)
- `ridge.clinic` (36)
- `stone.and.sons` (30)
- `lantern.row` (28)
- `alder.physio` (23)
- `pale.harbour` (21)
- `copper.studio` (19)

## Resolution — fixed
The engineering update on the Challenge page marks #4471 closed on 05 October. The parser is **fixed**: `fix(dates): parse dd/mm for eu locales`. Close this ticket as completed because engineering fixed this parser bug, not because the reports were split or documented.

## Notes
- Intake tags are noisy here: **23** parser reports were tagged `hint`.
- Desk notes mark **5** of these reports as one-day moves, but their tenant/channel behavior still places them with the parser bug.
