<script>
    let milesDaily;
    let vehicle;
    let annualFlights;
    let flightType;
</script>

<main>
	<h2>Transportation</h2>
    <form>
        <label for="miles-daily"><h3>Average Miles Driven Per Day</h3></label>
        <input type="range" id="miles-daily" name="miles-daily" min="0" max="200" bind:value={milesDaily}>
        {#if milesDaily != undefined}
            <p>{milesDaily}</p>
        {/if}
        <br>
        <h3>Vehicle Type</h3>
        <label for="sedan">Sedan/Coupe/Hatchback</label>
        <input type="radio" id="sedan" name="vehicle-type" value="sedan" on:click={() => {
            vehicle = "sedan";
        }}>
        <label for="suv">SUV/Minivan</label>
        <input type="radio" id="suv" name="vehicle-type" value="suv" on:click={() => {
            vehicle = "suv";
        }}>
        <label for="truck">Pickup Truck</label>
        <input type="radio" id="truck" name="vehicle-type" value="truck" on:click={() => {
            vehicle = "truck";
        }}>
        <label for="motorcycle">Motorcycle/3-Wheeler</label>
        <input type="radio" id="motorcycle" name="vehicle-type" value="motorcycle" on:click={() => {
            vehicle = "motorcycle";
        }}>
        <label for="n/a">N/A</label>
        <input type="radio" id="n/a" name="vehicle-type" value="n/a" on:click={() => {
            vehicle = "n/a";
        }}>
        <br>
        <label for="annual-flights"><h3>Average Time Flying Annually</h3></label>
        <input type="range" id="annual-flights" name="annual-flights" min="0" max="100" bind:value={annualFlights}>
        {#if annualFlights != undefined}
            <p>{annualFlights}</p>
        {/if}
        <br>
        <h3>Flight Type</h3>
        <label for="economy">Economy</label>
        <input type="radio" id="economy" name="flight-type" value="suv" on:click={() => {
            flightType = "economy";
        }}>
        <label for="business">Business</label>
        <input type="radio" id="business" name="flight-type" value="business" on:click={() => {
            flightType = "business";
        }}>
        <label for="first-class">First Class</label>
        <input type="radio" id="first-class" name="flight-type" value="first-class" on:click={() => {
            vehicle = "first-class";
        }}>
        <label for="n/a">N/A</label>
        <input type="radio" id="n/a" name="flight-type" value="n/a" on:click={() => {
            vehicle = "n/a";
        }}>
    </form>
</main>

<style>
</style>