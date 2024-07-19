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

    hundreds = Math.floor(delta / 100);
    delta = delta % 100;

    fifties = Math.floor(delta / 50);
    delta = delta % 50;

    twenties = Math.floor(delta / 20);
    remainder = delta % 20;

    prev = value;
  } else {
    // history pop
  }
</script>

<div class="h-full p-8 text-3xl font-bold flex-col relative">
	<div class="flex gap-1 h-1/3">
		{#each new Array(hundreds) as n}
		|
		{/each}
	</div>
	<div class="flex gap-1 h-1/3">
		{#each new Array(fifties) as n}
		|
		{/each}
	</div>
	<div class="flex gap-1 h-1/3">
		{#each new Array(twenties) as n}
			|
		{/each}
	</div>
	<div class="absolute top-1/2 right-4">
		{remainder}
	</div>
</div>
