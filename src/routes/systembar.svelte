<script lang="ts">
  export let P1: number;
  export let P2: number;
  export let openK1: boolean;
  export let openK2: boolean;
  export let history: [P1: number, P2: number][];
</script>

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
