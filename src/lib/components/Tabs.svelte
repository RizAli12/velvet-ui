<script>
  /**
   * VelvetUI — Tabs
   * @prop tabs   Array<{id, label}>  tab definitions  required
   * @prop active string  bind:active — active tab id  default: tabs[0].id
   *
   * Slots: tab-{id} for each panel
   *
   * Usage:
   *   <Tabs
   *     tabs={[
   *       { id: 'overview', label: 'Overview' },
   *       { id: 'code',     label: 'Code'     },
   *     ]}
   *     bind:active={tab}
   *   >
   *     {#snippet tab-overview()}<p>Overview content</p>{/snippet}
   *     {#snippet tab-code()}<pre>...</pre>{/snippet}
   *   </Tabs>
   */

  let { tabs = [], active = $bindable(''), snippets = {} } = $props();

  // default to first tab
  if (!active && tabs.length) active = tabs[0].id;
</script>

<div class="vui-tabs">
  <div class="vui-tabs__list" role="tablist">
    {#each tabs as tab}
      <button
        role="tab"
        class="vui-tabs__btn"
        class:vui-tabs__btn--active={active === tab.id}
        aria-selected={active === tab.id}
        aria-controls={`panel-${tab.id}`}
        id={`tab-${tab.id}`}
        onclick={() => (active = tab.id)}
      >
        {tab.label}
      </button>
    {/each}
  </div>

  {#each tabs as tab}
    <div
      role="tabpanel"
      id={`panel-${tab.id}`}
      aria-labelledby={`tab-${tab.id}`}
      hidden={active !== tab.id}
      class="vui-tabs__panel"
    >
      {@render snippets[tab.id]?.()}
    </div>
  {/each}
</div>

<style>
  .vui-tabs__list {
    display: flex;
    border-bottom: 1px solid var(--border);
    gap: 0;
  }

  .vui-tabs__btn {
    background: none;
    border: none;
    border-bottom: 2px solid transparent;
    color: var(--muted);
    padding: 0.6rem 1.1rem;
    font-family: inherit;
    font-size: 0.8rem;
    cursor: pointer;
    letter-spacing: 0.04em;
    margin-bottom: -1px;
    transition: color 0.2s, border-color 0.2s;
  }
  .vui-tabs__btn:hover  { color: var(--text); }
  .vui-tabs__btn:focus-visible { outline: 2px solid var(--gold); outline-offset: 2px; }
  .vui-tabs__btn--active { color: var(--gold); border-bottom-color: var(--gold); }

  .vui-tabs__panel {
    padding: 1.1rem 0;
    font-size: 0.82rem;
    color: var(--soft);
    animation: vui-fade-in 0.2s ease;
  }
  .vui-tabs__panel[hidden] { display: none; }

  @keyframes vui-fade-in { from { opacity: 0; } to { opacity: 1; } }
</style>
