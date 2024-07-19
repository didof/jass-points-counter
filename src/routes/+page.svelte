<script lang="ts">
  import Keyboard from "./keyboard.svelte";
  import Punkte from "./punkte.svelte";

  let P1 = 0;
  let openK1 = false;
  let P2 = 0;
  let openK2 = false;

  let history: [P1: number, P2: number][] = [[0, 0]];
</script>

<svelte:head>
  <title>Jass Punkte Zähler</title>
</svelte:head>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<div class="h-screen w-screen flex flex-col justify-between">
  <menu class="flex">
    <button
      on:click={() => {
        history.length = 0;
        P1 = 0;
        P2 = 0;
        openK1 = false;
        openK2 = false;
      }}
      class="px-6 py-3 text-xl font-semibold border"
    >
      reset
    </button>
    <button
      on:click={() => {
        history.pop();
        if (history.length == 0) return;
        const last = history.at(-1) || [0, 0];
        P1 = last[0];
        P2 = last[1];
      }}
      class="px-6 py-3 text-xl font-semibold border bg-blue-500"
    >
      undo
    </button>
  </menu>
  <div class="h-full grid grid-cols-1 grid-rows-2">
    <div class="border bg-blue-500/20 relative rotate-180">
      <div class="absolute inset-0" on:click={() => (openK1 = true)}>
        <Punkte value={P1} />
      </div>
      <Keyboard
        bind:open={openK1}
        bind:value={P1}
        on:change={() => {
          history.push([P1, P2]);
          history = history;
        }}
      />
    </div>
    <div class="border bg-blue-500/20 relative">
      <div class="absolute inset-0" on:click={() => (openK2 = true)}>
        <Punkte value={P2} />
      </div>
      <Keyboard
        bind:open={openK2}
        bind:value={P2}
        on:change={() => {
          history.push([P1, P2]);
          history = history;
        }}
      />
    </div>
  </div>
</div>
