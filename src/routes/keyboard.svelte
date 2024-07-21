<script lang="ts" context="module">
  const N = [1, 2, 3, 4, 5, 6, 7, 8, 9];
</script>

<script lang="ts">
  import Icon from "@iconify/svelte";
  import { createEventDispatcher } from "svelte";
  import { fly } from "svelte/transition";

  const dispatch = createEventDispatcher<{
    change: number;
  }>();

  let className = "";
  export { className as class };

  export let value: number;
  export let open: boolean;
  let p = "0";
  $: if (open) p = "0";
</script>

{#if open}
  <div
    transition:fly={{ duration: 200, y: 100 }}
    class="absolute inset-0 flex flex-col justify-between bg-gradient-to-b from-zinc-800/95 to-zinc-950/95 border-t-2 border-zinc-900/50 text-white {className}"
  >
    <div
      class="py-1 px-4 border-b-2 border-zinc-900/50 flex items-center justify-between"
    >
      <button
        class="opacity-60 font-semibold flex items-center justify-center gap-1 rounded-md"
        on:click={() => (open = false)}
      >
        <Icon icon="carbon:close-outline" />
        Schliessen
      </button>
      <span class="text-3xl font-bold tracking-widest">
        {p.replace(/^0+/, "") || "0"}
      </span>
    </div>
    <div class="grid grid-cols-3 flex-grow opacity-80">
      {#each N as n}
        <button class="text-2xl font-semibold" on:click={() => (p += n)}>
          {n}
        </button>
      {/each}
      <button
        class="grid place-content-center"
        on:click={() => (p = p.substring(0, p.length - 1))}
      >
        <div
          class="border-2 border-orange-700/30 bg-orange-500/10 text-orange-500 font-bold flex items-center gap-2 py-2 px-4 rounded-3xl"
        >
          <Icon icon="mdi:erase-outline" />
          Löschen
        </div>
      </button>
      <button class="text-2xl font-semibold" on:click={() => (p += 0)}>
        0
      </button>
      <button
        class="grid place-content-center"
        on:click={() => {
          value += parseInt(p, 10);
          dispatch("change", value);
          open = false;
        }}
      >
        <div
          class="border-2 border-emerald-700/30 bg-emerald-500/10 text-emerald-500 font-bold flex items-center gap-2 py-2 px-4 rounded-3xl"
        >
          <Icon icon="ph:check-bold" />
          OK
        </div>
      </button>
    </div>
  </div>
{/if}
