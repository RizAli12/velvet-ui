<script>
  /**
   * VelvetUI — Input
   * @prop label       string   field label        default: ''
   * @prop placeholder string                      default: ''
   * @prop type        string   html input type    default: 'text'
   * @prop error       string   validation message default: ''
   * @prop disabled    boolean                     default: false
   * @prop value       string   bind:value         default: ''
   *
   * Usage:
   *   <Input label="Email" bind:value={email} type="email" />
   *   <Input label="Name" error="Required" bind:value={name} />
   */

  let {
    label       = '',
    placeholder = '',
    type        = 'text',
    error       = '',
    disabled    = false,
    value       = $bindable(''),
  } = $props();

  let focused = $state(false);
  const uid = `vui-input-${Math.random().toString(36).slice(2, 8)}`;
</script>

<div class="vui-input-wrap">
  {#if label}
    <label for={uid} class="vui-input__label" class:vui-input__label--focused={focused}>
      {label}
    </label>
  {/if}

  <input
    id={uid}
    {type}
    {placeholder}
    {disabled}
    bind:value
    onfocus={() => (focused = true)}
    onblur={() => (focused = false)}
    class="vui-input__field"
    class:vui-input__field--focused={focused && !error}
    class:vui-input__field--error={!!error}
    aria-invalid={!!error}
    aria-describedby={error ? `${uid}-err` : undefined}
  />

  {#if error}
    <p id="{uid}-err" class="vui-input__error" role="alert">{error}</p>
  {/if}
</div>

<style>
  .vui-input-wrap {
    display: flex;
    flex-direction: column;
    gap: 0.4rem;
    width: 100%;
  }

  .vui-input__label {
    font-size: 0.68rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--muted);
    transition: color 0.2s;
    cursor: pointer;
  }
  .vui-input__label--focused { color: var(--gold); }

  .vui-input__field {
    width: 100%;
    background: var(--bg);
    border: 1px solid var(--border);
    color: var(--text);
    padding: 0.65rem 1rem;
    border-radius: 0.25rem;
    font-family: inherit;
    font-size: 0.85rem;
    outline: none;
    transition: border-color 0.2s, box-shadow 0.2s;
  }
  .vui-input__field::placeholder { color: var(--muted); }
  .vui-input__field:disabled     { opacity: 0.4; cursor: not-allowed; }

  .vui-input__field--focused {
    border-color: var(--gold);
    box-shadow: 0 0 0 3px rgba(200, 165, 90, 0.08);
  }
  .vui-input__field--error {
    border-color: var(--red);
    box-shadow: 0 0 0 3px rgba(212, 126, 126, 0.1);
  }

  .vui-input__error {
    font-size: 0.7rem;
    color: var(--red);
    margin: 0;
  }
</style>
