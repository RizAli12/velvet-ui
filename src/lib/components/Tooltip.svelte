<script>
  /**
   * VelvetUI — Tooltip
   * @prop text     string   tooltip content      required
   * @prop position 'top' | 'bottom' | 'left' | 'right'  default: 'top'
   * @prop delay    number   show delay ms        default: 120
   *
   * Usage:
   *   <Tooltip text="Opens settings panel">
   *     <Button>Settings</Button>
   *   </Tooltip>
   */

  const { text, position = 'top', delay = 120, children } = $props();

  let visible = $state(false);
  let timer;

  const show = () => { timer = setTimeout(() => (visible = true),  delay); };
  const hide = () => { clearTimeout(timer); visible = false; };
</script>

<span
  class="vui-tooltip-wrap"
  onmouseenter={show}
  onmouseleave={hide}
  onfocus={show}
  onblur={hide}
>
  {@render children?.()}

  {#if visible}
    <span class="vui-tooltip vui-tooltip--{position}" role="tooltip">
      {text}
      <span class="vui-tooltip__arrow"></span>
    </span>
  {/if}
</span>

<style>
  .vui-tooltip-wrap {
    position: relative;
    display: inline-flex;
    align-items: center;
  }

  .vui-tooltip {
    position: absolute;
    z-index: 50;
    background: var(--bg3);
    border: 1px solid var(--border);
    color: var(--text);
    font-size: 0.72rem;
    padding: 0.4rem 0.75rem;
    border-radius: 0.25rem;
    white-space: nowrap;
    pointer-events: none;
    animation: vui-tooltip-in 0.15s ease both;
    box-shadow: 0 4px 16px rgba(0,0,0,0.3);
    letter-spacing: 0.02em;
  }

  /* positions */
  .vui-tooltip--top    { bottom: calc(100% + 8px); left: 50%; transform: translateX(-50%); }
  .vui-tooltip--bottom { top:    calc(100% + 8px); left: 50%; transform: translateX(-50%); }
  .vui-tooltip--left   { right:  calc(100% + 8px); top: 50%;  transform: translateY(-50%); }
  .vui-tooltip--right  { left:   calc(100% + 8px); top: 50%;  transform: translateY(-50%); }

  /* arrows */
  .vui-tooltip__arrow {
    position: absolute;
    width: 0; height: 0;
    border: 4px solid transparent;
  }
  .vui-tooltip--top    .vui-tooltip__arrow { top: 100%;   left: 50%; transform: translateX(-50%); border-top-color: var(--border);    }
  .vui-tooltip--bottom .vui-tooltip__arrow { bottom: 100%; left: 50%; transform: translateX(-50%); border-bottom-color: var(--border); }
  .vui-tooltip--left   .vui-tooltip__arrow { left: 100%;  top: 50%;  transform: translateY(-50%); border-left-color: var(--border);   }
  .vui-tooltip--right  .vui-tooltip__arrow { right: 100%; top: 50%;  transform: translateY(-50%); border-right-color: var(--border);  }

  @keyframes vui-tooltip-in {
    from { opacity: 0; transform: translateX(-50%) scale(0.88); }
    to   { opacity: 1; transform: translateX(-50%) scale(1); }
  }
</style>
