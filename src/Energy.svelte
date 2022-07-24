<script>
    import { items } from "./stores.js";

    let residences = [{
            type: "residence",
            id: "house",
            name: "House",
            isChecked: false,
            value: 9525.64
        },
        {
            type: "residence",
            id: "mobile-home",
            name: "Mobile Home",
            isChecked: false,
            value: 9578.44
        },
        {
            type: "residence",
            id: "apartment-small",
            name: "Apartment With 2-4 Units",
            isChecked: false,
            value: 9387.84
        },
        {
            type: "residence",
            id: "apartment-large",
            name: "Apartment With 5+ Units",
            isChecked: false,
            value: 8001
        }    
    ];
    let prevPeople = 1;
    let people;
    let hasPanels = false;
    let solarPanels;

    let residenceClicked;
    let panelsClicked;

</script>

<main>
    <h2>Energy</h2>
    
    <h3>How Many People Live in Your Residence?</h3>
    <input type="range" id="residence" name="residence" min="1" max="10" bind:value={people} on:click={() => {
        for(let i = 0; i < residences.length; i++){
            residences[i].value *= prevPeople;
            residences[i].value /= people;
            prevPeople = 1;
        }
        prevPeople *= people;
    }}>
    {#if people != undefined}
        <p>{people}</p>
    {/if}

    {#if people !== undefined}
        <h3>Place of Residence</h3>

        {#each residences as {name, id}, i}
            <label for={id}>{name}</label>
            <input type="radio" id={id} name="residence" value={name} on:click={() => {
                if(residenceClicked === false){
                    $items = [...$items, residences[i]];  
                }
                else{
                    $items = $items.filter((e) => { return e.type !== "residence" });
                    $items = [...$items, residences[i]];    
                }
                residenceClicked = true;
            }}>
        {/each}
    {/if}

    <h3>Do You Own Solar Panels?</h3>
    <label for="hasPanels">Yes</label>
    <input type="radio" id="panelsYes" name="hasPanels" value="yes" on:click={() => {
        hasPanels = true;
    }}>
    <label for="hasPanels">No</label>
    <input type="radio" id="panelsNo" name="hasPanels" value="no" on:click={() => {
        hasPanels = false;
        if(panelsClicked === false){
            $items = [...$items, {
                type: "panels",
                name: "Number of Solar Panels",
                id: "panels",
                value: 0
            }]
        }
        else{
            $items = $items.filter((e) => { return e.type !== "panels" });
            $items = [...$items, {
                type: "panels",
                name: "Number of Solar Panels",
                id: "panels",
                value: 0
            }]
        }
        panelsClicked = true;
    }}>
    {#if hasPanels === true}
        <h3>What Percentage of Your Power is Produced by Your Solar Panels?</h3>
        <input type="range" id="solar-panels" name="solar-panels" min="1" max="100" bind:value={solarPanels} on:click={() => {
            if(panelsClicked === false){
                $items = [...$items, {
                    type: "panels",
                    name: "Number of Solar Panels",
                    id: "panels",
                    value: ((solarPanels / 100) * -1422.4)
                }]
            }
            else{
                $items = $items.filter((e) => { return e.type !== "panels" });
                $items = [...$items, {
                    type: "panels",
                    name: "Number of Solar Panels",
                    id: "panels",
                    value: ((solarPanels / 100) * -1422.4)
                }]
            }
            panelsClicked = true;
        }}>
        {#if solarPanels != undefined}
            <p>{solarPanels}</p>
        {/if}
    {/if}
</main>

<style>
    h2{
        text-decoration-color: #00BCCB;
    }
</style>