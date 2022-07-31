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
		<h1 id="result"><span>You have a Carbon Footprint of </span><br><span id="footprint">{footprint}</span><br><span> Grams of CO2 Per Year</span></h1>
	{:else if footprint !== undefined}
		<h1 id="result"><span>You have a Carbon Footprint of </span><br><span id="footprint">{footprint}</span><br><span>Gram Per Year</span></h1>
	{/if}

	<br>

</main>

<style>
	#submit{
		margin-left: 695px;
		margin-top: 5rem;
		margin-bottom: 5rem;
		background-color: #1c1d1f;
		border-color: #1c1d1f;
		color: white;
		border-radius: 5px;
		border-width: 2px;
		width: 500px;
		height: 100px;
		font-size: 2rem;
		transition: .3s ease;
	}
	
	#submit:hover{
		transition: .3s ease;
		border-color: white;
	}

	#submit:active{
		transform: translateY(5px);
	}

	#result{
		margin-left: 695px;
		background-color: #1c1d1f;
		width: 500px;
		padding: 10px;
		border-radius: 5px;
	}

	#footprint{
		font-size: 5rem;	
		position: fixed;
	}
</style>