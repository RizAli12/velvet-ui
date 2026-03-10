<script>
  import {
    Button,
    Badge,
    Input,
    Toggle,
    Loader,
    Card,
    Tooltip,
    Progress,
    Notification,
    Avatar,
    AvatarStack,
    Select,
    Tabs,
    Modal,
    Accordion,
    Skeleton,
    Stat,
  } from "$lib/index.js";

  let modalOpen = $state(false);
  let toggleOn = $state(true);
  let inputVal = $state("");
  let selectVal = $state("");
  let activeTab = $state("overview");

  const tabs = [
    { id: "overview", label: "Overview" },
    { id: "code", label: "Code" },
    { id: "props", label: "Props" },
  ];

  const accordionItems = [
    {
      id: "q1",
      title: "What's included?",
      content: "17 Svelte 5 components, pure CSS, MIT license.",
    },
    {
      id: "q2",
      title: "Is it accessible?",
      content: "Yes — keyboard nav, ARIA roles, WCAG 2.1 AA.",
    },
    {
      id: "q3",
      title: "Svelte 5 only?",
      content:
        "Yes — uses $props(), $state(), $derived(), snippets throughout.",
    },
  ];

  const users = [
    { initials: "AK", variant: "gold" },
    { initials: "SJ", variant: "blue" },
    { initials: "MR", variant: "green" },
    { initials: "LP", variant: "red" },
    { initials: "TW", variant: "gold" },
  ];

  const plans = [
    { value: "free", label: "Free" },
    { value: "pro", label: "Pro — $39" },
    { value: "team", label: "Team — $89" },
  ];
</script>

<div
  style="max-width:800px; margin:0 auto; padding:3rem 1.5rem; display:flex; flex-direction:column; gap:3rem;"
>
  <h1 style="font-size:2rem; color:var(--gold)">VelvetUI — Component Test</h1>

  <!-- Buttons -->
  <section>
    <h2>Buttons</h2>
    <div style="display:flex; gap:1rem; flex-wrap:wrap; margin-top:1rem">
      <Button variant="primary">Primary</Button>
      <Button variant="outlined">Outlined</Button>
      <Button variant="ghost">Ghost</Button>
      <Button variant="primary" loading>Loading</Button>
      <Button variant="outlined" disabled>Disabled</Button>
      <Button variant="primary" size="sm">Small</Button>
      <Button variant="primary" size="lg">Large</Button>
    </div>
  </section>

  <!-- Badges -->
  <section>
    <h2>Badges</h2>
    <div style="display:flex; gap:0.75rem; flex-wrap:wrap; margin-top:1rem">
      <Badge variant="gold" dot>Active</Badge>
      <Badge variant="blue">Info</Badge>
      <Badge variant="green" dot>Success</Badge>
      <Badge variant="red">Error</Badge>
      <Badge variant="muted" pill={false}>Tag</Badge>
    </div>
  </section>

  <!-- Inputs -->
  <section>
    <h2>Input</h2>
    <div
      style="display:flex; flex-direction:column; gap:1rem; margin-top:1rem; max-width:360px"
    >
      <Input
        label="Email"
        bind:value={inputVal}
        type="email"
        placeholder="you@example.com"
      />
      <Input
        label="With error"
        error="This field is required"
        bind:value={inputVal}
      />
      <p style="font-size:0.8rem; color:var(--muted)">Typed: {inputVal}</p>
    </div>
  </section>

  <!-- Toggle -->
  <section>
    <h2>Toggle</h2>
    <div
      style="display:flex; flex-direction:column; gap:0.75rem; margin-top:1rem"
    >
      <Toggle bind:checked={toggleOn} label="Dark mode" />
      <Toggle bind:checked={toggleOn} label="Notifications" />
      <Toggle disabled label="Disabled toggle" />
      <p style="font-size:0.8rem; color:var(--muted)">State: {toggleOn}</p>
    </div>
  </section>

  <!-- Loaders -->
  <section>
    <h2>Loaders</h2>
    <div
      style="display:flex; gap:2rem; align-items:center; flex-wrap:wrap; margin-top:1rem"
    >
      <Loader variant="spin" />
      <Loader variant="dots" />
      <Loader variant="pulse" />
      <Loader variant="bar" />
      <Loader variant="spin" color="var(--blue)" size="lg" />
    </div>
  </section>

  <!-- Card -->
  <section>
    <h2>Card</h2>
    <div style="max-width:320px; margin-top:1rem">
      <Card>
        {#snippet header()}<strong>Card Title</strong>{/snippet}
        <p style="font-size:0.85rem; color:var(--soft)">
          Hover me to see the lift and border glow.
        </p>
        {#snippet footer()}Released under MIT{/snippet}
      </Card>
    </div>
  </section>

  <!-- Tooltip -->
  <section>
    <h2>Tooltip</h2>
    <div style="display:flex; gap:1rem; flex-wrap:wrap; margin-top:1rem">
      <Tooltip text="Top tooltip (default)">
        <Button variant="outlined">Hover top</Button>
      </Tooltip>
      <Tooltip text="Bottom tooltip" position="bottom">
        <Button variant="outlined">Hover bottom</Button>
      </Tooltip>
      <Tooltip text="Right side" position="right">
        <Button variant="ghost">Hover right</Button>
      </Tooltip>
    </div>
  </section>

  <!-- Progress -->
  <section>
    <h2>Progress</h2>
    <div
      style="display:flex; flex-direction:column; gap:0.75rem; margin-top:1rem; max-width:400px"
    >
      <Progress value={78} label="Svelte" />
      <Progress value={54} label="TypeScript" color="var(--blue)" />
      <Progress value={91} label="CSS Animations" color="var(--green)" />
    </div>
  </section>

  <!-- Notifications -->
  <section>
    <h2>Notifications</h2>
    <div
      style="display:flex; flex-direction:column; gap:0.75rem; margin-top:1rem; max-width:420px"
    >
      <Notification variant="gold" title="Update available"
        >Version 2.1.0 is ready.</Notification
      >
      <Notification variant="green" title="Deployed!" dismiss
        >Your app is live.</Notification
      >
      <Notification variant="red" title="Build failed" dismiss
        >Check the logs for details.</Notification
      >
      <Notification variant="blue" title="Heads up"
        >New components are coming soon.</Notification
      >
    </div>
  </section>

  <!-- Avatars -->
  <section>
    <h2>Avatar + AvatarStack</h2>
    <div style="display:flex; flex-direction:column; gap:1rem; margin-top:1rem">
      <div style="display:flex; gap:0.75rem; align-items:center">
        <Avatar initials="AK" variant="gold" size="sm" />
        <Avatar initials="SJ" variant="blue" />
        <Avatar initials="MR" variant="green" size="lg" online />
        <Avatar initials="LP" variant="red" size="xl" />
      </div>
      <AvatarStack {users} max={3} />
    </div>
  </section>

  <!-- Select -->
  <section>
    <h2>Select</h2>
    <div style="max-width:280px; margin-top:1rem">
      <Select label="Billing plan" bind:value={selectVal} options={plans} />
      <p style="font-size:0.8rem; color:var(--muted); margin-top:0.5rem">
        Selected: {selectVal}
      </p>
    </div>
  </section>

  <!-- Tabs -->
  <section>
    <h2>Tabs</h2>
    <div style="margin-top:1rem; max-width:480px">
      <Tabs
        {tabs}
        bind:active={activeTab}
        snippets={{
          overview: () =>
            "High-level summary of the component and its purpose.",
          code: () => '<Button variant="primary">Click me</Button>',
          props: () => "variant · size · disabled · loading · type · onclick",
        }}
      />
    </div>
  </section>

  <!-- Modal -->
  <section>
    <h2>Modal</h2>
    <div style="margin-top:1rem">
      <Button onclick={() => (modalOpen = true)}>Open Modal</Button>
    </div>

    <Modal bind:open={modalOpen} title="Confirm action">
      <p>This will permanently delete the item. This cannot be undone.</p>
      {#snippet footer()}
        <Button variant="outlined" onclick={() => (modalOpen = false)}
          >Cancel</Button
        >
        <Button variant="primary" onclick={() => (modalOpen = false)}
          >Confirm</Button
        >
      {/snippet}
    </Modal>
  </section>

  <!-- Accordion -->
  <section>
    <h2>Accordion</h2>
    <div style="margin-top:1rem; max-width:500px">
      <Accordion items={accordionItems} />
    </div>
  </section>

  <!-- Skeleton -->
  <section>
    <h2>Skeleton</h2>
    <div
      style="display:flex; flex-direction:column; gap:0.5rem; margin-top:1rem; max-width:360px"
    >
      <div style="display:flex; gap:0.75rem; align-items:center">
        <Skeleton circle width="2.4rem" height="2.4rem" />
        <div style="flex:1; display:flex; flex-direction:column; gap:0.4rem">
          <Skeleton width="55%" height="10px" />
          <Skeleton width="35%" height="8px" />
        </div>
      </div>
      <Skeleton width="100%" />
      <Skeleton width="70%" />
      <Skeleton width="85%" />
    </div>
  </section>

  <!-- Stat -->
  <section>
    <h2>Stat Cards</h2>
    <div style="display:flex; gap:1rem; flex-wrap:wrap; margin-top:1rem">
      <Stat value="2.4k" label="Users" trend={12.4} />
      <Stat value="$8.2k" label="Revenue" trend={-3.1} color="var(--blue)" />
      <Stat value="99.9%" label="Uptime" trend={0.2} color="var(--green)" />
    </div>
  </section>
</div>

