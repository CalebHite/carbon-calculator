<script>
    import { items } from "./stores.js";
    import { Card, CardHeader, CardBody } from "sveltestrap";

    let vehicles = [
        {
            type: "vehicle",
            name: "Motorcycle/3-Wheeler",
            id: "motorcycle",
            value: 0.81,
            isClicked: false
        },
        {
            type: "vehicle",
            name: "Sedan/Coupe/Hatchback",
            id: "sedan",
            value: 0.87,
            isClicked: false
        },
        {
            type: "vehicle",
            name: "SUV/SUC/Minivan",
            id: "suv",
            value: .93,
            isClicked: false
        },
        {
            type: "vehicle",
            name: "Pickup Truck",
            id: "truck",
            value: 0.88,
            isClicked: false
        },
        {
            type: "vehicle",
            name: "Diesel Truck",
            id: "diesel",
            value: 2.01,
            isClicked: false
        },
        {
            type: "vehicle",
            name: "Walk/Bike/Skate",
            id: "walk",
            value: 0,
            isClicked: false
        }
    ];
    
    let flights = [
        {
            type: "flight",
            name: "Economy",
            id: "economy",
            value: 158.73
        },
        {
            type: "flight",
            name: "Business",
            id: "business",
            value: 238.1
        },
        {
            type: "flight",
            name: "First Class",
            id: "first-class",
            value: 317.47
        },
        {
            type: "flight",
            name: "N/A",
            id: "n/a",
            value: 0
        }
    ]

    let milesDaily;
    let annualFlights;

    let vehicleClicked = false;
    let milesClicked = false;
    let flightClicked = false;
    let flyingClicked = false;

    let vehicleEmissions = false;
    let takenFlights = false;

    let prevMiles = 1;
    let prevFlight = 1;
</script>

<main>
    <h2>Transportation</h2>

    <Card id="card1">
        <CardHeader>
            <h3>What Type of Transportation Do You Use Most Often?</h3>
        </CardHeader>   
        <CardBody> 
            <div class="options vehicles">
                {#each vehicles as {name, id}, i}
                    <div class="input">
                        <label for={id}>{name}</label>
                    <input type="radio" id={id} name="vehicle-type" value={name} on:click={() => {
                        if(vehicleClicked === false){
                            $items = [...$items, vehicles[i]];
                            vehicleClicked = true;
                        }
                        else{
                            $items = $items.filter((e) => { return e.type !== "vehicle" });
                            $items = [...$items, vehicles[i]];
                        }
                        if(vehicles[i].id !== "walk"){
                            vehicleEmissions = true;
                        }
                        else{
                            vehicleEmissions = false;
                        }
                        vehicleClicked === true;
                    }}>
                    </div>
                {/each}
            </div>
        </CardBody>
    </Card>
    {#if vehicleEmissions === true}
        <Card id="card2">
            <CardHeader>
                <label for="miles-daily"><h3>Average Miles Driven Per Day</h3></label>
            </CardHeader>
            <CardBody>
                <div class="input miles">
                        <input type="range" id="miles-daily" name="miles-daily" min="1" max="200" bind:value={milesDaily} on:click={()=>{
                            if(milesClicked === false){
                                for(let i = 0; i < vehicles.length; i++){
                                    vehicles[i].value *= (milesDaily * 365);
                                }
                            }
                            else{
                                for(let i = 0; i < vehicles.length; i++){
                                    vehicles[i].value /= (prevMiles * 365);
                                    vehicles[i].value *= (milesDaily * 365);
                                }
                                prevMiles = 1;
                                prevMiles *= milesDaily; 
                            }

                            milesClicked = true;
                        }}>
                </div>
                {#if milesDaily !== undefined}
                    <p class="range-text">{milesDaily}</p>
                {/if}
            </CardBody>
        </Card>
    {/if}
    <Card id="card3">
        <CardHeader>
            <h3>How Do You Fly Most Often?</h3>
        </CardHeader>
        <CardBody>
            <div class="options flights">
                {#each flights as {name, id}, i}
                    <div class="input">
                        <label for={id}>{name}</label>
                        <input type="radio" id={id} name="flight-type" value={name} on:click={() => {
                            if(flightClicked === false){
                                $items = [...$items, flights[i]];
                                flightClicked = true;
                            }
                            else{
                                $items = $items.filter((e) => { return e.type !== "flight" });
                                $items = [...$items, flights[i]];
                            }
                            
                            if(flights[i].id !== "n/a"){
                                takenFlights = true;
                            }
                            else{
                                takenFlights = false;
                            }

                            flightClicked === true;
                        }}>
                    </div>
                {/each}
            </div>
        </CardBody>
    </Card>
    {#if takenFlights === true}
        <Card id="card4">
            <CardHeader>
                <label for="annual-flights"><h3>Average Time Flying Annually (Hours)</h3></label>
            </CardHeader>
            <CardBody>
                <div class="input flights">
                    <input type="range" id="annual-flights" name="annual-flights" min="1" max="500" bind:value={annualFlights} on:click={()=>{
                    if(flyingClicked === false){
                        for(let i = 0; i < flights.length; i++){
                            flights[i].value *= annualFlights;
                        }
                    }
                    else{
                        for(let i = 0; i < flights.length; i++){
                            flights[i].value /= prevFlight;
                            flights[i].value *= annualFlights;
                        }
                        prevFlight = 1;
                        prevFlight *= annualFlights; 
                    }
                        flyingClicked = true;
                    }}>
                </div>
                {#if annualFlights != undefined}
                    <p class="range-text">{annualFlights}</p>
                {/if}
            </CardBody>
        </Card>
    {/if}
</main>

<style>
    h2{
        text-decoration-color: #EF0079;
    }
    input {
        accent-color: #EF0079;
    }
</style>