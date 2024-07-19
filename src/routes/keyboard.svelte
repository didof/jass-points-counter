<script lang="ts" context="module">
  const N = [1, 2, 3, 4, 5, 6, 7, 8, 9];
</script>

<script lang="ts">
  import { createEventDispatcher } from "svelte";

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
    class="absolute inset-0 flex flex-col justify-between bg-black text-white {className}"
  >
    <div class="text-3xl font-bold tracking-widest text-center py-1">
      {p.replace(/^0+/, "") || "0"}
    </div>
    <div class="grid grid-cols-3 flex-grow">
      {#each N as n}
        <button class="border text-2xl font-semibold" on:click={() => (p += n)}>
          {n}
        </button>
      {/each}
      <button
        class="border text-2xl font-semibold bg-red-500"
        on:click={() => (open = false)}
      >
        cancel
      </button>
      <button class="border text-2xl font-semibold" on:click={() => (p += 0)}
        >0</button
      >
      <button
        class="border text-2xl font-semibold bg-orange-500"
        on:click={() => {
          p = p.substring(0, p.length - 1);
        }}
      >
        x
      </button>
      <button
        class="border text-2xl font-semibold col-span-3 bg-green-500"
        on:click={() => {
          value += parseInt(p, 10);
          dispatch("change", value);
          open = false;
        }}
      >
        OK
      </button>
    </div>
  </div>
{/if}
