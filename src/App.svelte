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
	<button type="submit" on:click={submit} id="submit">Submit Form</button>

	{#if footprint !== undefined && footprint !== 1 && footprint !== -1}
		<h1>You have a Carbon Footprint of {footprint} Grams of CO2 Per Year</h1>
	{:else if footprint !== undefined}
		<h1>You have a Carbon Footprint of {footprint} Gram Per Year</h1>
	{/if}

</main>

<style>
	#submit{
		margin-left: 690px;
		margin-top: 5rem;
		margin-bottom: 5rem;
		background-color: #1c1d1f;
		color: white;
		border-radius: 5px;
		border-width: 1px;
		width: 500px;
		height: 100px;
		font-size: 2rem;
		transition: .5s ease-in-out;
	}
	
	#submit:hover{
		transition: .5s ease-in-out;
		background-color: rgb(47, 49, 49);
	}
	#submit:active {
		transform: translateY(4px);
	}
</style>