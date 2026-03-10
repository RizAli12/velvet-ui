<script>
  /**
   * VelvetUI — Skeleton
   * @prop width   string  css width   default: '100%'
   * @prop height  string  css height  default: '12px'
   * @prop radius  string  css border-radius  default: '0.25rem'
   * @prop circle  boolean perfect circle     default: false
   *
   * Usage:
   *   <Skeleton width="60%" />
   *   <Skeleton circle width="2.4rem" height="2.4rem" />
   */

  const { width = '100%', height = '12px', radius = '0.25rem', circle = false } = $props();

  const style = [
    `width:${width}`,
    `height:${height}`,
    `border-radius:${circle ? '50%' : radius}`,
  ].join(';');
</script>

<span class="vui-skeleton" style={style} aria-hidden="true"></span>

<style>
  .vui-skeleton {
    display: block;
    background: linear-gradient(
      90deg,
      var(--bg3, #14161c) 25%,
      rgba(255,255,255,0.04) 50%,
      var(--bg3, #14161c) 75%
    );
    background-size: 200% 100%;
    animation: vui-shimmer 1.5s infinite;
    flex-shrink: 0;
  }

  @keyframes vui-shimmer {
    from { background-position: 200% 0; }
    to   { background-position: -200% 0; }
  }
</style>
