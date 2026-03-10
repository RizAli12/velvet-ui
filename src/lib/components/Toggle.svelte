<script>
  /**
   * VelvetUI — Toggle
   * @prop checked  boolean bind:checked   default: false
   * @prop label    string  visible label  default: ''
   * @prop disabled boolean               default: false
   *
   * Usage:
   *   <Toggle bind:checked={darkMode} label="Dark mode" />
   */

  let { checked = $bindable(false), label = '', disabled = false } = $props();
  const uid = `vui-toggle-${Math.random().toString(36).slice(2, 8)}`;
</script>

<div class="vui-toggle-wrap">
  <button
    role="switch"
    id={uid}
    aria-checked={checked}
    aria-label={label || 'Toggle'}
    {disabled}
    onclick={() => { if (!disabled) checked = !checked; }}
    class="vui-toggle"
    class:vui-toggle--on={checked}
    class:vui-toggle--disabled={disabled}
  >
    <span class="vui-toggle__thumb"></span>
  </button>

  {#if label}
    <label for={uid} class="vui-toggle__label">{label}</label>
  {/if}
</div>

<style>
  .vui-toggle-wrap {
    display: flex;
    align-items: center;
    gap: 0.75rem;
  }

  .vui-toggle {
    position: relative;
    width: 2.6rem;
    height: 1.4rem;
    background: var(--bg3);
    border: 1px solid var(--border);
    border-radius: 999px;
    cursor: pointer;
    transition: background 0.25s, border-color 0.25s;
    flex-shrink: 0;
    padding: 0;
  }
  .vui-toggle:focus-visible { outline: 2px solid var(--gold); outline-offset: 3px; }
  .vui-toggle--on  { background: var(--gold); border-color: var(--gold); }
  .vui-toggle--disabled { opacity: 0.4; cursor: not-allowed; }

  .vui-toggle__thumb {
    position: absolute;
    top: 3px;
    left: 3px;
    width: 14px;
    height: 14px;
    background: #fff;
    border-radius: 50%;
    transition: transform 0.25s cubic-bezier(0.4, 0, 0.2, 1);
    pointer-events: none;
  }
  .vui-toggle--on .vui-toggle__thumb { transform: translateX(1.2rem); }

  .vui-toggle__label {
    font-size: 0.82rem;
    color: var(--soft);
    cursor: pointer;
    user-select: none;
  }
</style>
