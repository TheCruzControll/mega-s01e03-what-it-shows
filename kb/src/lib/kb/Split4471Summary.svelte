<script lang="ts">
  import reports from '#lib/data/reports-4471.json';
  import notes from '#lib/data/desk-notes.json';
  import { groupByCause, readAs, uniqueById, type Report } from '#lib/kb/causes';
  import { tenantOf } from '#lib/kb/locales';

  let { ticket }: { ticket: number } = $props();

  const allRows = reports as Report[];
  const merged = $derived(uniqueById(allRows).filter((r) => r.mergedInto === ticket));
  const duplicates = $derived(allRows.length - merged.length);
  const groups = $derived(groupByCause(merged, tenantOf));
  const groupOf = (cause: 'parser' | 'hint') => groups.find((g) => g.cause === cause);
  const channels = (cause: 'parser' | 'hint') => {
    const g = groupOf(cause);
    if (!g) return '';
    const counts = g.reports.reduce<Record<string, number>>((m, r) => ({ ...m, [r.channel]: (m[r.channel] ?? 0) + 1 }), {});
    return Object.entries(counts)
      .sort((a, b) => a[0].localeCompare(b[0]))
      .map(([channel, n]) => `${channel} ${n}`)
      .join(' · ');
  };
</script>

<p>
  The export has <strong>{allRows.length}</strong> rows for <strong>{merged.length}</strong> unique reports,
  so <strong>{duplicates}</strong> duplicate rows drop out by report id.
</p>

<table>
  <thead>
    <tr><th>problem</th><th>reports</th><th>tenants</th><th>channels</th><th>notes</th></tr>
  </thead>
  <tbody>
    {#if groupOf('parser')}
      <tr>
        <td><code>parser</code></td>
        <td>{groupOf('parser')?.reports.length}</td>
        <td>{groupOf('parser')?.tenants}</td>
        <td>{channels('parser')}</td>
        <td>Shared parser reads day-first tenant dates month first.</td>
      </tr>
    {/if}
    {#if groupOf('hint')}
      <tr>
        <td><code>hint</code></td>
        <td>{groupOf('hint')?.reports.length}</td>
        <td>{groupOf('hint')?.tenants}</td>
        <td>{channels('hint')}</td>
        <td><code>booking-v3</code> shows <code>MM/DD/YYYY</code> to day-first tenants.</td>
      </tr>
    {/if}
  </tbody>
</table>

{#if groupOf('parser')}
  {@const moved = readAs(groupOf('parser'), notes.oneDayMove)}
  {#if moved}
    <p class="note">{moved} parser reports were read as one-day moves, but the tenant and channel still place them with the parser bug.</p>
  {/if}
{/if}

<style>
  .note { color: var(--muted); font-size: 0.85em; }
</style>
