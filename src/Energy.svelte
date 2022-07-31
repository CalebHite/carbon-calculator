<script>
    import { Card, CardBody, CardHeader } from "sveltestrap";
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
    
    <Card id="card1">
        <CardHeader>
            <h3>How Many People Live in Your Residence?</h3>
        </CardHeader>
        <CardBody>
            <div class="options">
                <input type="range" id="residence" name="residence" min="1" max="10" bind:value={people} on:click={() => {
                    for(let i = 0; i < residences.length; i++){
                        residences[i].value *= prevPeople;
                        residences[i].value /= people;
                        prevPeople = 1;
                    }
                    prevPeople *= people;
                }}>
            </div>
            {#if people != undefined}
                <p class="range-text">{people}</p>
            {/if}
        </CardBody>
    </Card>
    {#if people !== undefined}
        <Card id="card2">
            <CardHeader>
                <h3>Place of Residence</h3>
            </CardHeader>
            <CardBody>
                <div class="options">
                    {#each residences as {name, id}, i}
                        <div class="input">
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
                        </div>
                    {/each}
                </div>
            </CardBody>
        </Card>
    {/if}
    <Card id="card3">
        <CardHeader>
            <h3>Do You Own Solar Panels?</h3>
        </CardHeader>
        <CardBody>
            <div class="options">
                <div class="input">
                    <label for="hasPanels">Yes</label>
                    <input type="radio" id="panelsYes" name="hasPanels" value="yes" on:click={() => {
                        hasPanels = true;
                    }}>
                </div>
                <div class="input">
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
                </div>
            </div>
        </CardBody>
    </Card>
    {#if hasPanels === true}
        <Card id="card3">
            <CardHeader>
                <h3>What Percentage of Your Power is Produced by Your Solar Panels?</h3>
            </CardHeader>
            <CardBody>
                <div class="input"> 
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
                </div>
                {#if solarPanels != undefined}
                    <p class="range-text">{solarPanels}</p>
                {/if}
            </CardBody>
        </Card>
    {/if}
</main>

<style>
    h2 {
        text-decoration-color: #00BCCB;
    }
    input {
        accent-color: #00BCCB;
    }

</style>