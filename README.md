# S01E03 · what it shows

This repo contains the split of support ticket **#4471** into the two distinct date problems found in the exported kb data.

## GitHub issues filed here

- **Date parser reads day-first tenant dates as month-first** — **379 reports**
- **booking-v3 date hint tells day-first tenants to type month-first** — **33 reports**

## KB deliverables

- Source page: `kb/src/routes/kb/incidents/4471-split/+page.svx`
- Rendered page: `rendered/4471-split.html`

## Notes

- The export contained **427 rows** but only **412 unique report ids**.
- **15 rows** were duplicate export overlap.
- This repo records the final split after work on **#4471** was done.
