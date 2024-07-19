<script lang="ts" context="module">
  const N = [1, 2, 3, 4, 5, 6, 7, 8, 9];
</script>

<script lang="ts">
  import Icon from "@iconify/svelte";

  import { createEventDispatcher } from "svelte";
  import { cubicInOut } from "svelte/easing";
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
    class="absolute inset-0 flex flex-col justify-between bg-gradient-to-b from-zinc-800/90 to-zinc-950/90 border-t-2 border-zinc-900 text-white {className}"
  >
    <div class="text-3xl font-bold tracking-widest text-right py-1 px-4 border-b-2 border-zinc-900">
      {p.replace(/^0+/, "") || "0"}
    </div>
    <div class="grid grid-cols-3 flex-grow opacity-80">
      {#each N as n}
        <button class="text-2xl font-semibold" on:click={() => (p += n)}>
          {n}
        </button>
      {/each}
      <button
        class="text-xl font-semibold bg-rose-900 flex items-center justify-center gap-1 rounded-tr-md"
        on:click={() => (open = false)}
      >
        <Icon icon="carbon:close-outline" />
        Schliessen
      </button>
      <button class="text-2xl font-semibold" on:click={() => (p += 0)}>
        0
      </button>
      <button
        class="text-xl font-semibold bg-orange-900 flex items-center justify-center gap-1 rounded-tl-md"
        on:click={() => {
          p = p.substring(0, p.length - 1);
        }}
      >
        <Icon icon="mdi:erase-outline" />
        Löschen
      </button>
      <button
        class="text-xl font-semibold col-span-3 bg-emerald-800 flex items-center justify-center gap-1"
        on:click={() => {
          value += parseInt(p, 10);
          dispatch("change", value);
          open = false;
        }}
      >
        <Icon icon="ph:check-bold" />
        OK
      </button>
    </div>
  </div>
{/if}
