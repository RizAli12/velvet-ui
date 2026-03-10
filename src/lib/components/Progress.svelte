<script>
  /**
   * VelvetUI — Progress
   * @prop value   number  0–100          required
   * @prop label   string  left label     default: ''
   * @prop color   css color              default: 'var(--gold)'
   * @prop height  number  px height      default: 4
   * @prop animate boolean entrance anim default: true
   *
   * Usage:
   *   <Progress value={72} label="Svelte" />
   *   <Progress value={48} label="TypeScript" color="var(--blue)" />
   */

  const {
    value   = 0,
    label   = '',
    color   = 'var(--gold)',
    height  = 4,
    animate = true,
  } = $props();

  const pct = Math.min(100, Math.max(0, value));
</script>

<div class="vui-progress">
  {#if label}
    <div class="vui-progress__header">
      <span class="vui-progress__label">{label}</span>
      <span class="vui-progress__value" style="color:{color}">{pct}%</span>
    </div>
  {/if}

  <div
    class="vui-progress__track"
    style="height:{height}px"
    role="progressbar"
    aria-valuenow={pct}
    aria-valuemin={0}
    aria-valuemax={100}
    aria-label={label || 'Progress'}
  >
    <div
      class="vui-progress__fill"
      class:vui-progress__fill--animate={animate}
      style="width:{pct}%; background:{color};"
    ></div>
  </div>
</div>

<style>
  .vui-progress { display: flex; flex-direction: column; gap: 0.4rem; width: 100%; }

  .vui-progress__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .vui-progress__label { font-size: 0.75rem; color: var(--muted); }
  .vui-progress__value { font-size: 0.72rem; font-weight: 500; }

  .vui-progress__track {
    background: var(--border, rgba(255,255,255,0.07));
    border-radius: 999px;
    overflow: hidden;
    width: 100%;
  }

  .vui-progress__fill {
    height: 100%;
    border-radius: 999px;
    transition: width 0.6s ease;
  }
  .vui-progress__fill--animate {
    animation: vui-fill-in 0.9s cubic-bezier(0.4, 0, 0.2, 1) both;
  }

  @keyframes vui-fill-in {
    from { width: 0 !important; }
  }
</style>
