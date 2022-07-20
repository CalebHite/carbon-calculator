<script>
	import Transportation from "./Transportation.svelte";
	import Energy from "./Energy.svelte";
	import Food from "./Food.svelte";
	import Plants from "./Plants.svelte";

	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	var amounts = [];

</script>

<main>
	<h1>Carbon Footprint Calculator</h1>
	<Transportation {amounts}/>
	<Energy {amounts} />
	<Food {amounts}/>
	<Plants {amounts}/>
	<button type="submit">Submit Form</button>
</main>

<style>
</style>