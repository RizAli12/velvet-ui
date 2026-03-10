<script>
  /**
   * VelvetUI — Stat Card
   * @prop value  string  large display value   required
   * @prop label  string  small descriptor      default: ''
   * @prop trend  number  positive/negative %   default: null
   * @prop color  css color for value           default: 'var(--gold)'
   *
   * Usage:
   *   <Stat value="2.4k" label="Users"   trend={12.4} />
   *   <Stat value="$8.2k" label="Revenue" color="var(--blue)" />
   */

  const { value, label = '', trend = null, color = 'var(--gold)' } = $props();
  const positive = $derived(trend !== null && trend >= 0);
</script>

<div class="vui-stat">
  <span class="vui-stat__value" style="color:{color}">{value}</span>

  <div class="vui-stat__footer">
    {#if label}<span class="vui-stat__label">{label}</span>{/if}
    {#if trend !== null}
      <span class="vui-stat__trend" class:vui-stat__trend--up={positive} class:vui-stat__trend--down={!positive}>
        {positive ? '▲' : '▼'} {Math.abs(trend)}%
      </span>
    {/if}
  </div>
</div>

<style>
  .vui-stat {
    background: var(--bg3);
    border: 1px solid var(--border);
    border-radius: 0.4rem;
    padding: 1.1rem 1.3rem;
    display: flex; flex-direction: column; gap: 0.35rem;
    transition: border-color 0.2s, transform 0.2s;
    cursor: default;
  }
  .vui-stat:hover { border-color: var(--border-h); transform: translateY(-2px); }

  .vui-stat__value {
    font-family: 'Playfair Display', Georgia, serif;
    font-size: 1.7rem; font-weight: 700; line-height: 1;
  }

  .vui-stat__footer { display: flex; align-items: center; justify-content: space-between; gap: 0.5rem; }

  .vui-stat__label {
    font-size: 0.68rem; text-transform: uppercase;
    letter-spacing: 0.08em; color: var(--muted);
  }

  .vui-stat__trend { font-size: 0.68rem; font-weight: 600; }
  .vui-stat__trend--up   { color: var(--green); }
  .vui-stat__trend--down { color: var(--red);   }
</style>
