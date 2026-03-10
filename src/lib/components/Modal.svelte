<script>
  /**
   * VelvetUI — Modal
   * @prop open     boolean  bind:open           default: false
   * @prop title    string   modal heading       default: ''
   * @prop width    string   css max-width       default: '420px'
   * @prop closable boolean  click-outside/esc   default: true
   *
   * Slots: default (body), footer
   *
   * Usage:
   *   <Modal bind:open={showModal} title="Confirm action">
   *     <p>Are you sure?</p>
   *     {#snippet footer()}
   *       <Button onclick={() => showModal = false}>Confirm</Button>
   *     {/snippet}
   *   </Modal>
   */

  import { fade, scale } from "svelte/transition";
  import { cubicOut } from "svelte/easing";

  let {
    open = $bindable(false),
    title = "",
    width = "420px",
    closable = true,
    footer,
    children,
  } = $props();

  const close = () => {
    if (closable) open = false;
  };

  // close on Escape
  const onKeydown = (e) => {
    if (e.key === "Escape") close();
  };
</script>

<svelte:window onkeydown={onKeydown} />

{#if open}
  <!-- overlay -->
  <div
    transition:fade={{ duration: 200 }}
    class="vui-modal-overlay"
    onclick={close}
    aria-hidden="true"
  ></div>

  <!-- dialog -->
  <div
    transition:scale={{ duration: 250, start: 0.92, easing: cubicOut }}
    class="vui-modal"
    style="max-width:{width}"
    role="dialog"
    aria-modal="true"
    aria-labelledby={title ? "vui-modal-title" : undefined}
  >
    <div class="vui-modal__header">
      {#if title}
        <h2 id="vui-modal-title" class="vui-modal__title">{title}</h2>
      {/if}
      {#if closable}
        <button class="vui-modal__close" onclick={close} aria-label="Close"
          >✕</button
        >
      {/if}
    </div>

    <div class="vui-modal__body">{@render children?.()}</div>

    {#if footer}
      <div class="vui-modal__footer">{@render footer()}</div>
    {/if}
  </div>
{/if}

<style>
  .vui-modal-overlay {
    position: fixed;
    inset: 0;
    z-index: 200;
    background: rgba(0, 0, 0, 0.65);
    backdrop-filter: blur(4px);
  }

  .vui-modal {
    position: fixed;
    z-index: 201;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: calc(100% - 2rem);
    background: var(--bg3);
    border: 1px solid var(--border);
    border-radius: 0.5rem;
    box-shadow: 0 24px 80px rgba(0, 0, 0, 0.5);
    overflow: hidden;
  }

  .vui-modal__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1.2rem 1.4rem 0;
  }
  .vui-modal__title {
    font-family: "Playfair Display", Georgia, serif;
    font-size: 1.05rem;
    font-weight: 700;
    margin: 0;
  }
  .vui-modal__close {
    background: none;
    border: none;
    cursor: pointer;
    color: var(--muted);
    font-size: 0.75rem;
    padding: 0.2rem;
    transition: color 0.2s;
    line-height: 1;
  }
  .vui-modal__close:hover {
    color: var(--red);
  }

  .vui-modal__body {
    padding: 1rem 1.4rem 1.2rem;
    font-size: 0.85rem;
    color: var(--soft);
  }
  .vui-modal__footer {
    padding: 0.9rem 1.4rem;
    border-top: 1px solid var(--border);
    display: flex;
    gap: 0.6rem;
    justify-content: flex-end;
  }
</style>
