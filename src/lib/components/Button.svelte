<script>
  /**
   * VelvetUI — Button
   * @prop variant  'primary' | 'outlined' | 'ghost'   default: 'primary'
   * @prop size     'sm' | 'md' | 'lg'                 default: 'md'
   * @prop disabled boolean                             default: false
   * @prop loading  boolean                             default: false
   * @prop type     'button' | 'submit' | 'reset'      default: 'button'
   * @prop onclick  event handler
   *
   * Usage:
   *   <Button variant="primary" onclick={() => alert('hi')}>Save</Button>
   *   <Button variant="outlined" loading>Saving…</Button>
   */

  const {
    variant  = 'primary',
    size     = 'md',
    disabled = false,
    loading  = false,
    type     = 'button',
    onclick,
    children,
  } = $props();
</script>

<button
  {type}
  class="vui-btn vui-btn--{variant} vui-btn--{size}"
  disabled={disabled || loading}
  aria-busy={loading}
  {onclick}
>
  {#if loading}
    <span class="vui-btn__spinner" aria-hidden="true"></span>
    <span class="sr-only">Loading…</span>
  {/if}
  {@render children?.()}
</button>

<style>
  .vui-btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    font-family: inherit;
    font-weight: 500;
    letter-spacing: 0.03em;
    border-radius: 0.25rem;
    border: 1px solid transparent;
    cursor: pointer;
    user-select: none;
    text-decoration: none;
    transition: transform 0.18s ease, box-shadow 0.18s ease,
                background 0.18s ease, border-color 0.18s ease, color 0.18s ease;
    position: relative;
    white-space: nowrap;
  }
  .vui-btn:focus-visible {
    outline: 2px solid var(--gold);
    outline-offset: 3px;
  }
  .vui-btn:disabled {
    opacity: 0.4;
    pointer-events: none;
  }

  /* variants */
  .vui-btn--primary {
    background: var(--gold);
    color: #0a0b0e;
    border-color: var(--gold);
  }
  .vui-btn--primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 28px rgba(200, 165, 90, 0.38);
    background: var(--gold2);
  }
  .vui-btn--primary:active { transform: translateY(0); }

  .vui-btn--outlined {
    background: transparent;
    color: var(--text);
    border-color: var(--border);
  }
  .vui-btn--outlined:hover {
    border-color: var(--border-h);
    color: var(--gold);
    transform: translateY(-2px);
  }

  .vui-btn--ghost {
    background: rgba(126, 181, 212, 0.1);
    color: var(--blue);
    border-color: rgba(126, 181, 212, 0.25);
  }
  .vui-btn--ghost:hover {
    background: rgba(126, 181, 212, 0.2);
    transform: translateY(-2px);
  }

  /* sizes */
  .vui-btn--sm { padding: 0.35rem 0.85rem; font-size: 0.75rem; }
  .vui-btn--md { padding: 0.6rem 1.4rem;   font-size: 0.85rem; }
  .vui-btn--lg { padding: 0.8rem 2rem;     font-size: 0.95rem; }

  /* spinner */
  .vui-btn__spinner {
    display: inline-block;
    width: 0.85em;
    height: 0.85em;
    border: 2px solid currentColor;
    border-top-color: transparent;
    border-radius: 50%;
    animation: vui-spin 0.7s linear infinite;
    flex-shrink: 0;
  }

  .sr-only {
    position: absolute;
    width: 1px; height: 1px;
    padding: 0; margin: -1px;
    overflow: hidden; clip: rect(0,0,0,0);
    white-space: nowrap; border: 0;
  }

  @keyframes vui-spin { to { transform: rotate(360deg); } }
</style>
