<script>
  /**
   * VelvetUI — Select
   * @prop options  Array<{value, label}>  option list  required
   * @prop value    string  bind:value                  default: ''
   * @prop label    string  field label                 default: ''
   * @prop disabled boolean                             default: false
   * @prop placeholder string                           default: 'Select…'
   *
   * Usage:
   *   <Select
   *     bind:value={plan}
   *     label="Billing plan"
   *     options={[
   *       { value: 'free',  label: 'Free' },
   *       { value: 'pro',   label: 'Pro — $39' },
   *     ]}
   *   />
   */

  let {
    options     = [],
    value       = $bindable(''),
    label       = '',
    disabled    = false,
    placeholder = 'Select…',
  } = $props();

  let focused = $state(false);
  const uid = `vui-select-${Math.random().toString(36).slice(2, 8)}`;
</script>

<div class="vui-select-wrap">
  {#if label}
    <label for={uid} class="vui-select__label" class:vui-select__label--focused={focused}>
      {label}
    </label>
  {/if}

  <div class="vui-select__box">
    <select
      id={uid}
      {disabled}
      bind:value
      onfocus={() => (focused = true)}
      onblur={() => (focused = false)}
      class="vui-select__field"
      class:vui-select__field--focused={focused}
    >
      <option value="" disabled>{placeholder}</option>
      {#each options as opt}
        <option value={opt.value}>{opt.label}</option>
      {/each}
    </select>
    <span class="vui-select__arrow" aria-hidden="true">▾</span>
  </div>
</div>

<style>
  .vui-select-wrap { display: flex; flex-direction: column; gap: 0.4rem; width: 100%; }

  .vui-select__label {
    font-size: 0.68rem; text-transform: uppercase;
    letter-spacing: 0.1em; color: var(--muted); transition: color 0.2s;
  }
  .vui-select__label--focused { color: var(--gold); }

  .vui-select__box { position: relative; }

  .vui-select__field {
    width: 100%;
    appearance: none;
    background: var(--bg);
    border: 1px solid var(--border);
    color: var(--text);
    padding: 0.65rem 2.4rem 0.65rem 1rem;
    border-radius: 0.25rem;
    font-family: inherit;
    font-size: 0.85rem;
    outline: none;
    cursor: pointer;
    transition: border-color 0.2s, box-shadow 0.2s;
  }
  .vui-select__field:disabled { opacity: 0.4; cursor: not-allowed; }
  .vui-select__field--focused  {
    border-color: var(--gold);
    box-shadow: 0 0 0 3px rgba(200, 165, 90, 0.08);
  }

  .vui-select__arrow {
    position: absolute;
    right: 0.8rem; top: 50%;
    transform: translateY(-50%);
    color: var(--muted);
    pointer-events: none;
    font-size: 0.65rem;
  }
</style>
