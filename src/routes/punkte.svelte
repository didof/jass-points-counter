<script lang="ts">
  export let value: number;
  let prev = 0;
  let hundreds = 0;
  let fifties = 0;
  let twenties = 0;
  let remainder = 0;
  $: if (prev < value) {
    // normal use
    let delta = value - prev;

    hundreds += Math.floor(delta / 100);
    delta = delta % 100;

    fifties += Math.floor(delta / 50);
    delta = delta % 50;

    twenties += Math.floor(delta / 20);
    remainder += delta % 20;

    prev = value;
  } else {
    let tmp = value;
    hundreds = Math.floor(tmp / 100);
    tmp = tmp % 100;

    fifties = Math.floor(tmp / 50);
    tmp = tmp % 50;

    twenties = Math.floor(tmp / 20);
    remainder = tmp % 20;

    prev = tmp;
  }
</script>

<div class="h-full p-8 relative">
  {#if value > 0}
    <div class="h-full flex flex-col justify-between">
      <div class="h-1/5 flex gap-1">
        {#each new Array(hundreds) as n}
          <div class="h-full w-1 bg-white" />
        {/each}
      </div>
      <div class="h-1/5 flex gap-1 -ml-8">
        {#each new Array(fifties) as _, i}
          <div
            class="h-full w-1 bg-white {i % 2 == 0
              ? 'rotate-[20deg] translate-x-1 ml-8'
              : '-rotate-[20deg] -translate-x-0.5'}"
          />
        {/each}
      </div>
      <div class="h-1/5 flex gap-1">
        {#each new Array(twenties) as n}
          <div class="h-full w-1 bg-white" />
        {/each}
      </div>
    </div>
    <div class="absolute top-1/2 right-4">
      {remainder}
    </div>
  {:else}
    <div
      class="w-max text-center flex flex-col text-lg absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2"
    >
      <span>drücken, um mit dem Hinzufügen </span>
      <span>von Punkten zu beginnen</span>
    </div>
  {/if}
</div>
