<script>
	import { items } from "./stores.js";
	import Transportation from "./Transportation.svelte";
	import Energy from "./Energy.svelte";
	import Food from "./Food.svelte";
	import Plants from "./Plants.svelte";

	function submit(){
		console.log($items);
	}
</script>

<main>
	<h1>Carbon Footprint Calculator</h1>
	<Transportation />
	<Energy />
	<Food />
	<Plants />
	<button type="submit" on:click={submit}>Submit Form</button>
</main>

<style>

</style>