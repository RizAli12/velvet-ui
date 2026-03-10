<script>
  /**
   * VelvetUI — AvatarStack
   * @prop users   Array<{initials, src?, variant?}>  user list  required
   * @prop max     number  visible before +N badge              default: 4
   * @prop size    'sm' | 'md' | 'lg'                           default: 'md'
   *
   * Usage:
   *   <AvatarStack
   *     users={[
   *       { initials: 'AK', variant: 'gold'  },
   *       { initials: 'SJ', variant: 'blue'  },
   *       { initials: 'MR', variant: 'green' },
   *     ]}
   *     max={3}
   *   />
   */

  import Avatar from './Avatar.svelte';

  const { users = [], max = 4, size = 'md' } = $props();

  const visible  = $derived(users.slice(0, max));
  const overflow = $derived(users.length - max);
</script>

<div class="vui-avatar-stack" aria-label={`${users.length} members`}>
  {#each visible as user}
    <div class="vui-avatar-stack__item">
      <Avatar
        initials={user.initials}
        src={user.src ?? ''}
        alt={user.initials}
        variant={user.variant ?? 'gold'}
        {size}
      />
    </div>
  {/each}

  {#if overflow > 0}
    <div class="vui-avatar-stack__item vui-avatar-stack__more vui-avatar-stack__more--{size}">
      +{overflow}
    </div>
  {/if}
</div>

<style>
  .vui-avatar-stack { display: flex; align-items: center; }

  .vui-avatar-stack__item {
    margin-left: -0.6rem;
    border: 2px solid var(--bg2, #0f1115);
    border-radius: 50%;
    transition: transform 0.2s;
  }
  .vui-avatar-stack__item:first-child { margin-left: 0; }
  .vui-avatar-stack__item:hover { transform: translateY(-3px); z-index: 1; }

  .vui-avatar-stack__more {
    display: flex; align-items: center; justify-content: center;
    border-radius: 50%;
    background: var(--bg3);
    border-color: var(--border);
    color: var(--muted);
    font-size: 0.65rem;
    font-weight: 600;
    letter-spacing: 0.03em;
    flex-shrink: 0;
  }
  .vui-avatar-stack__more--sm { width: 1.75rem; height: 1.75rem; }
  .vui-avatar-stack__more--md { width: 2.4rem;  height: 2.4rem;  }
  .vui-avatar-stack__more--lg { width: 3rem;    height: 3rem;    }
</style>
