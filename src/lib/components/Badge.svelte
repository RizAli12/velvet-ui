<script>
  /**
   * VelvetUI — Badge
   * @prop variant 'gold' | 'blue' | 'green' | 'red' | 'muted'  default: 'gold'
   * @prop dot     boolean  live indicator pulse dot              default: false
   * @prop pill    boolean  fully rounded pill                    default: true
   *
   * Usage:
   *   <Badge variant="green" dot>Active</Badge>
   *   <Badge variant="red">Error</Badge>
   */

  const { variant = 'gold', dot = false, pill = true, children } = $props();
</script>

<span class="vui-badge vui-badge--{variant}" class:vui-badge--pill={pill} role="status">
  {#if dot}
    <span class="vui-badge__dot" aria-hidden="true"></span>
  {/if}
  {@render children?.()}
</span>

<style>
  .vui-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.35rem;
    padding: 0.25rem 0.65rem;
    font-size: 0.68rem;
    font-weight: 500;
    letter-spacing: 0.05em;
    border: 1px solid transparent;
    border-radius: 0.2rem;
    line-height: 1;
  }
  .vui-badge--pill { border-radius: 999px; }

  .vui-badge--gold  { background: rgba(200,165,90,0.12);  color: var(--gold);  border-color: rgba(200,165,90,0.22);  }
  .vui-badge--blue  { background: rgba(126,181,212,0.10); color: var(--blue);  border-color: rgba(126,181,212,0.22); }
  .vui-badge--green { background: rgba(125,196,160,0.10); color: var(--green); border-color: rgba(125,196,160,0.22); }
  .vui-badge--red   { background: rgba(212,126,126,0.10); color: var(--red);   border-color: rgba(212,126,126,0.22); }
  .vui-badge--muted { background: var(--bg3);             color: var(--muted); border-color: var(--border);          }

  .vui-badge__dot {
    width: 0.45rem;
    height: 0.45rem;
    border-radius: 50%;
    background: currentColor;
    animation: vui-pulse 1.4s ease-in-out infinite;
    flex-shrink: 0;
  }

  @keyframes vui-pulse {
    0%, 100% { opacity: 1;   transform: scale(1);   }
    50%       { opacity: 0.5; transform: scale(1.35); }
  }
</style>
