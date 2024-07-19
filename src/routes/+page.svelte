<script lang="ts">
  import Keyboard from "./keyboard.svelte";
  import Punkte from "./punkte.svelte";
  import Systembar from "./systembar.svelte";

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
<div
  class="h-screen w-screen flex flex-col justify-between"
  style="height: 100svh;"
>
  <div class="h-full grid grid-cols-1 grid-rows-2 blackboard">
    <div class="relative rotate-180">
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
    <div class="relative">
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
  <Systembar bind:P1 bind:P2 bind:openK1 bind:openK2 bind:history />
</div>

<style lang="postcss">
  .blackboard {
    @apply bg-stone-950 bg-cover bg-center text-white;
    background-image: url(/blackboard.png);
  }
</style>
