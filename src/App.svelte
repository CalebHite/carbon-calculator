<script>
	import { items } from "./stores.js";
	import Transportation from "./Transportation.svelte";
	import Energy from "./Energy.svelte";
	import Food from "./Food.svelte";
	import Plants from "./Plants.svelte";

	let footprint;

	function submit(){
		footprint = 0;
		for(let i = 0; i < $items.length; i++){
			footprint += $items[i].value;
			footprint = Math.round(footprint * 10) / 10;
		}
	}
</script>

<main>
	<h1>Carbon Footprint Calculator</h1>
	<Transportation />
	<Energy />
	<Food />
	<Plants />
	<button type="submit" on:click={submit}>Submit Form</button>

	{#if footprint !== undefined && footprint !== 1 && footprint !== -1}
		<h1>You have a Carbon Footprint of {footprint} Grams Per Year</h1>
	{:else if footprint !== undefined}
		<h1>You have a Carbon Footprint of {footprint} Gram Per Year</h1>
	{/if}

</main>

<style>

</style>