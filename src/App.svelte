<script>
	import Transportation from "./Transportation.svelte";
	import Energy from "./Energy.svelte";
	import Food from "./Food.svelte";
	import Plants from "./Plants.svelte";

	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	var items = [];

	function submit(){
		console.log("hi");
	}
</script>

<main>
	<h1>Carbon Footprint Calculator</h1>
	<Transportation {items}/>
	<Energy {items} />
	<Food {items}/>
	<Plants {items}/>
	<button type="submit" on:click={submit}>Submit Form</button>
</main>

<style>
</style>