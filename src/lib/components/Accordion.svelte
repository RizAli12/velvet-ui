<script>
  /**
   * VelvetUI — Accordion
   * @prop items   Array<{id, title, content}>  sections  required
   * @prop single  boolean  close others on open          default: true
   *
   * Usage:
   *   <Accordion items={[
   *     { id: 'a', title: "What's included?", content: "22 components…" },
   *     { id: 'b', title: 'Is it accessible?', content: 'Yes — WCAG 2.1 AA' },
   *   ]} />
   */

  const { items = [], single = true } = $props();

  let open = $state(new Set());

  const toggle = (id) => {
    const next = new Set(open);
    if (next.has(id)) {
      next.delete(id);
    } else {
      if (single) next.clear();
      next.add(id);
    }
    open = next;
  };
</script>

<div class="vui-accordion" role="list">
  {#each items as item}
    {@const isOpen = open.has(item.id)}
    <div class="vui-accordion__item" role="listitem">
      <button
        class="vui-accordion__header"
        class:vui-accordion__header--open={isOpen}
        aria-expanded={isOpen}
        aria-controls={`acc-body-${item.id}`}
        id={`acc-btn-${item.id}`}
        onclick={() => toggle(item.id)}
      >
        <span>{item.title}</span>
        <span class="vui-accordion__icon" aria-hidden="true">▾</span>
      </button>

      <div
        id={`acc-body-${item.id}`}
        role="region"
        aria-labelledby={`acc-btn-${item.id}`}
        class="vui-accordion__body"
        class:vui-accordion__body--open={isOpen}
      >
        <div class="vui-accordion__content">{item.content}</div>
      </div>
    </div>
  {/each}
</div>

<style>
  .vui-accordion {
    border: 1px solid var(--border);
    border-radius: 0.35rem;
    overflow: hidden;
    width: 100%;
  }

  .vui-accordion__item + .vui-accordion__item {
    border-top: 1px solid var(--border);
  }

  .vui-accordion__header {
    width: 100%; background: none; border: none;
    display: flex; justify-content: space-between; align-items: center;
    padding: 0.9rem 1rem;
    color: var(--text); font-family: inherit; font-size: 0.82rem;
    cursor: pointer; text-align: left;
    transition: background 0.2s;
  }
  .vui-accordion__header:hover { background: rgba(255,255,255,0.025); }
  .vui-accordion__header:focus-visible { outline: 2px solid var(--gold); outline-offset: -2px; }
  .vui-accordion__header--open .vui-accordion__icon { transform: rotate(180deg); color: var(--gold); }

  .vui-accordion__icon {
    color: var(--muted);
    font-size: 0.65rem;
    transition: transform 0.25s ease, color 0.2s;
    flex-shrink: 0;
  }

  .vui-accordion__body {
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.32s ease;
  }
  .vui-accordion__body--open { max-height: 400px; }

  .vui-accordion__content {
    padding: 0.25rem 1rem 1rem;
    font-size: 0.8rem;
    color: var(--soft);
    line-height: 1.65;
  }
</style>
