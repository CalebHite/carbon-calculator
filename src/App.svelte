<script>
	import Transportation from "./Transportation.svelte";
	import Energy from "./Energy.svelte";
	import Food from "./Food.svelte";
	import Plants from "./Plants.svelte";

	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function submit(){
		// idk
	}
</script>

<main>
	<h1>Carbon Footprint Calculator</h1>
	<Transportation />
	<Energy  />
	<Food />
	<Plants />
	<button type="submit" on:click={submit}>Submit Form</button>
</main>

<style>
</style>