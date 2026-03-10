<script>
  /**
   * VelvetUI — Card
   * @prop hover   boolean  lift + glow on hover  default: true
   * @prop padding 'sm' | 'md' | 'lg'             default: 'md'
   *
   * Slots: header, default (body), footer
   *
   * Usage:
   *   <Card>
   *     {#snippet header()}<h3>Title</h3>{/snippet}
   *     <p>Content here</p>
   *   </Card>
   */

  const { hover = true, padding = 'md', header, footer, children } = $props();
</script>

<div class="vui-card vui-card--pad-{padding}" class:vui-card--hover={hover}>
  {#if header}
    <div class="vui-card__header">{@render header()}</div>
  {/if}

  <div class="vui-card__body">{@render children?.()}</div>

  {#if footer}
    <div class="vui-card__footer">{@render footer()}</div>
  {/if}
</div>

<style>
  .vui-card {
    background: var(--bg3);
    border: 1px solid var(--border);
    border-radius: 0.4rem;
    overflow: hidden;
    transition: border-color 0.25s, transform 0.25s, box-shadow 0.25s;
  }
  .vui-card--hover:hover {
    border-color: var(--border-h);
    transform: translateY(-3px);
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.35);
  }

  .vui-card--pad-sm .vui-card__body { padding: 0.85rem; }
  .vui-card--pad-md .vui-card__body { padding: 1.35rem; }
  .vui-card--pad-lg .vui-card__body { padding: 2rem; }

  .vui-card__header {
    padding: 1rem 1.35rem 0;
    font-weight: 500;
    font-size: 0.9rem;
  }
  .vui-card__footer {
    padding: 0 1.35rem 1rem;
    border-top: 1px solid var(--border);
    margin-top: 0.75rem;
    padding-top: 0.75rem;
    font-size: 0.78rem;
    color: var(--muted);
  }
</style>
