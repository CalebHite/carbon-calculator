<script>
    let milesDaily;
    let annualFlights;

    let vehicles = [
        {
            type: "vehicle",
            name: "Motorcycle/3-Wheeler",
            id: "motorcycle",
            value: 0
        },
        {
            type: "vehicle",
            name: "Sedan/Coupe/Hatchback",
            id: "sedan",
            value: 0
        },
        {
            type: "vehicle",
            name: "SUV/SUC/Minivan",
            id: "suv",
            value: 0
        },
        {
            type: "vehicle",
            name: "Pickup Truck",
            id: "truck",
            value: 0
        },
        {
            type: "vehicle",
            name: "Diesel Vehicle",
            id: "diesel",
            value: 0
        },
        {
            type: "vehicle",
            name: "N/A",
            id: "n/a",
            value: 0
        }
    ];
    
    let flights = [
        {
            type: "flight",
            name: "Economy",
            id: "economy",
            value: 0
        },
        {
            type: "flight",
            name: "Business",
            id: "business",
            value: 0
        },
        {
            type: "flight",
            name: "First Class",
            id: "first-class",
            value: 0
        },
        {
            type: "flight",
            name: "N/A",
            id: "n/a",
            value: 0
        }
    ]

    var transItems = [];
</script>

<main>
	<h2>Transportation</h2>
    <form>
        <label for="miles-daily"><h3>Average Miles Driven Per Day</h3></label>
        <input type="range" id="miles-daily" name="miles-daily" min="0" max="200" bind:value={milesDaily} on:click={()=>{
            transItems = transItems.filter((e) => { return e.type !== "miles" });
            transItems.push({
                type: "miles",
                name: "Miles Daily",
                id: "miles-daily",
                value: (milesDaily * 1)
            })
        }}>

        {#if milesDaily != undefined}
            <p>{milesDaily}</p>
        {/if}
        <br>
        {#each vehicles as {name, id}, i}
            <label for={id}>{name}</label>
            <input type="radio" id={id} name="vehicle-type" value={name} on:click={() => {
                transItems = transItems.filter((e) => { return e.type !== "vehicle" });
                transItems.push(vehicles[i]);
            }}>
        {/each}
        <br>
        <label for="annual-flights"><h3>Average Time Flying Annually (Hours)</h3></label>
        <input type="range" id="annual-flights" name="annual-flights" min="0" max="500" bind:value={annualFlights} on:click={()=>{
            transItems = transItems.filter((e) => { return e.type !== "flightTime" });
            transItems.push({
                type: "flightTime",
                name: "Flight Time Annually",
                id: "flight-time",
                value: (annualFlights * 1)
            })
        }}>
        {#if annualFlights != undefined}
            <p>{annualFlights}</p>
        {/if}      
        <br>
        <h3>Flight Type</h3>
        {#each flights as {name, id}, i}
            <label for={id}>{name}</label>
            <input type="radio" id={id} name="flight-type" value={name} on:click={() => {
                transItems = transItems.filter((e) => { return e.type !== "flight" });
                transItems.push(flights[i]);
            }}>
        {/each}
    </form>
</main>

<style>
    h2{
        text-decoration-color: #EF0079;
    }
</style>