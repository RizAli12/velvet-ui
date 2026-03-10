<script>
  /**
   * VelvetUI — Avatar
   * @prop initials string  2-letter fallback text  default: '?'
   * @prop src      string  image URL               default: ''
   * @prop alt      string  img alt text            default: initials
   * @prop size     'sm' | 'md' | 'lg' | 'xl'      default: 'md'
   * @prop variant  'gold' | 'blue' | 'green' | 'red'  default: 'gold'
   * @prop online   boolean green presence ring     default: false
   *
   * Usage:
   *   <Avatar initials="AK" variant="gold" online />
   *   <Avatar src="/me.jpg" alt="Profile photo" size="lg" />
   */

  const {
    initials = '?',
    src      = '',
    alt      = initials,
    size     = 'md',
    variant  = 'gold',
    online   = false,
  } = $props();

  let imgError = $state(false);
  const showImg = $derived(!!src && !imgError);
</script>

<span class="vui-avatar vui-avatar--{size} vui-avatar--{variant}" class:vui-avatar--online={online}>
  {#if showImg}
    <img src={src} alt={alt} onerror={() => (imgError = true)} />
  {:else}
    <span class="vui-avatar__initials" aria-label={alt}>{initials}</span>
  {/if}

  {#if online}
    <span class="vui-avatar__badge" aria-label="Online"></span>
  {/if}
</span>

<style>
  .vui-avatar {
    position: relative;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    border: 1.5px solid transparent;
    overflow: visible;
    flex-shrink: 0;
  }

  .vui-avatar img {
    width: 100%; height: 100%;
    border-radius: 50%;
    object-fit: cover;
    display: block;
  }

  .vui-avatar__initials {
    font-size: 0.72em;
    font-weight: 600;
    letter-spacing: 0.04em;
    text-transform: uppercase;
  }

  /* sizes */
  .vui-avatar--sm { width: 1.75rem; height: 1.75rem; }
  .vui-avatar--md { width: 2.4rem;  height: 2.4rem;  }
  .vui-avatar--lg { width: 3rem;    height: 3rem;    }
  .vui-avatar--xl { width: 4rem;    height: 4rem;    }

  /* variants */
  .vui-avatar--gold  { background: rgba(200,165,90,0.18);  color: var(--gold);  border-color: rgba(200,165,90,0.3);  }
  .vui-avatar--blue  { background: rgba(126,181,212,0.14); color: var(--blue);  border-color: rgba(126,181,212,0.28);}
  .vui-avatar--green { background: rgba(125,196,160,0.14); color: var(--green); border-color: rgba(125,196,160,0.28);}
  .vui-avatar--red   { background: rgba(212,126,126,0.12); color: var(--red);   border-color: rgba(212,126,126,0.25);}

  /* online badge */
  .vui-avatar__badge {
    position: absolute;
    bottom: 1px; right: 1px;
    width: 0.55rem; height: 0.55rem;
    background: var(--green);
    border-radius: 50%;
    border: 1.5px solid var(--bg);
  }
</style>
