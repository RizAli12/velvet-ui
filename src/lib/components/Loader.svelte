<script>
  /**
   * VelvetUI — Loader
   * @prop variant 'spin' | 'dots' | 'bar' | 'pulse'  default: 'spin'
   * @prop size    'sm' | 'md' | 'lg'                  default: 'md'
   * @prop color   css color string                     default: 'var(--gold)'
   *
   * Usage:
   *   <Loader variant="dots" />
   *   <Loader variant="bar" size="lg" />
   */

  const { variant = 'spin', size = 'md', color = 'var(--gold)' } = $props();
</script>

<span class="vui-loader vui-loader--{variant} vui-loader--{size}" style="--c:{color}" role="status" aria-label="Loading">
  {#if variant === 'dots'}
    <span></span><span></span><span></span>
  {:else if variant === 'bar'}
    <span class="vui-loader__bar-inner"></span>
  {/if}
</span>

<style>
  .vui-loader { display: inline-flex; align-items: center; justify-content: center; }

  /* spin */
  .vui-loader--spin {
    border: 2px solid rgba(255,255,255,0.1);
    border-top-color: var(--c);
    border-radius: 50%;
    animation: vui-spin 0.75s linear infinite;
  }
  .vui-loader--spin.vui-loader--sm { width: 1rem;   height: 1rem; }
  .vui-loader--spin.vui-loader--md { width: 1.75rem; height: 1.75rem; }
  .vui-loader--spin.vui-loader--lg { width: 2.5rem;  height: 2.5rem; }

  /* pulse */
  .vui-loader--pulse {
    background: var(--c);
    border-radius: 50%;
    animation: vui-pulse-loader 1.2s ease-in-out infinite;
  }
  .vui-loader--pulse.vui-loader--sm { width: 0.6rem;  height: 0.6rem; }
  .vui-loader--pulse.vui-loader--md { width: 0.9rem;  height: 0.9rem; }
  .vui-loader--pulse.vui-loader--lg { width: 1.25rem; height: 1.25rem; }

  /* dots */
  .vui-loader--dots { gap: 0.35rem; }
  .vui-loader--dots span {
    background: var(--c);
    border-radius: 50%;
    animation: vui-bounce 1.1s ease-in-out infinite;
  }
  .vui-loader--dots span:nth-child(2) { animation-delay: 0.15s; }
  .vui-loader--dots span:nth-child(3) { animation-delay: 0.30s; }
  .vui-loader--dots.vui-loader--sm span { width: 0.35rem; height: 0.35rem; }
  .vui-loader--dots.vui-loader--md span { width: 0.5rem;  height: 0.5rem;  }
  .vui-loader--dots.vui-loader--lg span { width: 0.7rem;  height: 0.7rem;  }

  /* bar */
  .vui-loader--bar {
    background: var(--border, rgba(255,255,255,0.07));
    border-radius: 999px;
    overflow: hidden;
  }
  .vui-loader--bar.vui-loader--sm { width: 80px;  height: 2px; }
  .vui-loader--bar.vui-loader--md { width: 120px; height: 3px; }
  .vui-loader--bar.vui-loader--lg { width: 180px; height: 4px; }
  .vui-loader__bar-inner {
    display: block;
    height: 100%;
    width: 40%;
    background: var(--c);
    border-radius: 999px;
    animation: vui-bar 1.4s ease-in-out infinite;
  }

  @keyframes vui-spin  { to { transform: rotate(360deg); } }
  @keyframes vui-pulse-loader {
    0%, 100% { transform: scale(1);    opacity: 1;   }
    50%       { transform: scale(1.45); opacity: 0.55; }
  }
  @keyframes vui-bounce {
    0%, 80%, 100% { transform: translateY(0); }
    40%           { transform: translateY(-6px); }
  }
  @keyframes vui-bar {
    0%   { transform: translateX(-100%); }
    100% { transform: translateX(350%); }
  }
</style>
