<script>
  /**
   * VelvetUI — Notification / Alert
   * @prop variant  'gold' | 'blue' | 'green' | 'red'  default: 'gold'
   * @prop title    string                              default: ''
   * @prop icon     string  emoji or text icon         default: auto
   * @prop dismiss  boolean show close button          default: false
   *
   * Slots: default (message body)
   *
   * Usage:
   *   <Notification variant="green" title="Deployed!" dismiss>
   *     Your changes are live in production.
   *   </Notification>
   */

  const { variant = 'gold', title = '', icon, dismiss = false, children } = $props();

  let visible = $state(true);

  const icons = { gold: 'ℹ', blue: '✦', green: '✓', red: '✕' };
  const displayIcon = icon ?? icons[variant] ?? icons.gold;
</script>

{#if visible}
  <div class="vui-notif vui-notif--{variant}" role="alert" aria-live="polite">
    <span class="vui-notif__icon" aria-hidden="true">{displayIcon}</span>

    <div class="vui-notif__body">
      {#if title}<strong class="vui-notif__title">{title}</strong>{/if}
      <span class="vui-notif__msg">{@render children?.()}</span>
    </div>

    {#if dismiss}
      <button
        class="vui-notif__close"
        aria-label="Dismiss"
        onclick={() => (visible = false)}
      >✕</button>
    {/if}
  </div>
{/if}

<style>
  .vui-notif {
    display: flex;
    align-items: flex-start;
    gap: 0.75rem;
    padding: 0.85rem 1rem;
    border-radius: 0.3rem;
    border: 1px solid var(--border);
    border-left-width: 3px;
    background: var(--bg3);
    animation: vui-slide-in 0.3s ease both;
    width: 100%;
  }

  .vui-notif--gold  { border-left-color: var(--gold);  }
  .vui-notif--blue  { border-left-color: var(--blue);  }
  .vui-notif--green { border-left-color: var(--green); }
  .vui-notif--red   { border-left-color: var(--red);   }

  .vui-notif__icon {
    font-size: 0.75rem;
    width: 1.3rem;
    height: 1.3rem;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    margin-top: 0.05rem;
  }
  .vui-notif--gold  .vui-notif__icon { background: rgba(200,165,90,0.12);  color: var(--gold);  }
  .vui-notif--blue  .vui-notif__icon { background: rgba(126,181,212,0.12); color: var(--blue);  }
  .vui-notif--green .vui-notif__icon { background: rgba(125,196,160,0.12); color: var(--green); }
  .vui-notif--red   .vui-notif__icon { background: rgba(212,126,126,0.12); color: var(--red);   }

  .vui-notif__body  { flex: 1; display: flex; flex-direction: column; gap: 0.2rem; }
  .vui-notif__title { font-size: 0.8rem; font-weight: 600; display: block; margin-bottom: 0.1rem; }
  .vui-notif__msg   { font-size: 0.76rem; color: var(--muted); }

  .vui-notif__close {
    background: none; border: none; cursor: pointer;
    color: var(--muted); font-size: 0.7rem;
    padding: 0; line-height: 1;
    transition: color 0.2s; flex-shrink: 0;
  }
  .vui-notif__close:hover { color: var(--red); }

  @keyframes vui-slide-in {
    from { opacity: 0; transform: translateX(-10px); }
    to   { opacity: 1; transform: translateX(0); }
  }
</style>
