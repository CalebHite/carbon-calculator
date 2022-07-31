<script>
    import { Card, CardBody, CardHeader } from "sveltestrap";
import { items } from "./stores.js";

    let hasTrees = false;
    let hasGarden = false;
    let percFood;
    let trees;

    let treesClicked = false;
    let gardenClicked = false;
</script>

<main>
    <h2>Plants</h2>
    <Card id="card1">
        <CardHeader>
            <h3>Do You Have Trees on Your Property?</h3>
        </CardHeader>
        <CardBody>
            <div class="options">
                <div class="input">
                    <label for="hasTrees">Yes</label>
                    <input type="radio" id="treesYes" name="hasTrees" value="yes" on:click={() => {
                        hasTrees = true;
                    }}>
                </div>
                <div class="input">
                    <label for="hasTrees">No</label>
                    <input type="radio" id="treesNo" name="hasTrees" value="no" on:click={() => {
                        hasTrees = false;
                        if(treesClicked === false){
                            $items = [...$items, {
                                type: "trees",
                                name: "Trees",
                                id: "trees",
                                value: 0
                            }];
                        }
                        else{
                            $items = $items.filter((e) => { return e.type !== "trees" });
                            $items = [...$items, {
                                type: "trees",
                                name: "Trees",
                                id: "trees",
                                value: 0
                            }];
                        }
                        treesClicked = true;
                    }}>
                </div>
            </div>
        </CardBody>
    </Card>
    {#if hasTrees === true}
        <Card id="card2">
            <CardHeader>
                <h3>How Many?</h3>
            </CardHeader>
            <CardBody>
                <div class="input">
                        <input type="range" id="trees" name="trees" min="1" max="200" bind:value={trees} on:click={()=>{
                        if(treesClicked === false){
                            $items = [...$items, {
                                type: "trees",
                                name: "Trees",
                                id: "trees",
                                value: (trees * -48)
                            }]
                        }
                        else{
                            $items = $items.filter((e) => { return e.type !== "trees" });
                            $items = [...$items, {
                                type: "trees",
                                name: "Trees",
                                id: "trees",
                                value: (trees * -48)
                            }]
                        }
                        treesClicked = true;
                    }}>
                </div>
                {#if trees != undefined}
                    <p class="range-text">{trees}</p>
                {/if}
            </CardBody>
        </Card>
    {/if}

    <Card id="card3">
        <CardHeader>
            <h3>Do You Own a Garden?</h3>
        </CardHeader>
        <CardBody>
            <div class="options">
                <label for="hasGarden">Yes</label>
                <input type="radio" id="gardenYes" name="hasGarden" value="yes" on:click={() => {
                    hasGarden = true;
                }}>
        
                <label for="hasGarden">No</label>
                <input type="radio" id="gardenYes" name="hasGarden" value="no" on:click={() => {
                    hasGarden = false;
                    if(gardenClicked === false){
                        $items = [...$items, {
                            type: "garden",
                            name: "Garden",
                            id: "garden",
                            value: 0
                        }];
                    }
                    else{
                        $items = $items.filter((e) => { return e.type !== "garden" });
                        $items = [...$items, {
                            type: "garden",
                            name: "Garden",
                            id: "garden",
                            value: 0
                        }];
                    }
                    gardenClicked = true;
                }}>
            </div>
        </CardBody>
    </Card>
    
    {#if hasGarden === true}
        <Card id="card4">
            <CardHeader>
                <h3>What Percent of Your Food Do You Grow?</h3>
            </CardHeader>
            <CardBody>
                <div class="options">
                    <input type="range" id="percFood" name="percFood" min="1" max="100" bind:value={percFood} on:click={()=>{
                        if(gardenClicked === false){
                            $items = [...$items, {
                                type: "garden",
                                name: "Garden",
                                id: "garden",
                                value: (( percFood / 100 ) * -4000)
                            }];
                        }
                        else{
                            $items = $items.filter((e) => { return e.type !== "garden" });
                            $items = [...$items, {
                                type: "garden",
                                name: "Garden",
                                id: "garden",
                                value: (( percFood / 100 ) * -4000)
                            }];
                        }
                        gardenClicked = true;
                    }}>
                </div>
                {#if percFood != undefined}
                <p class="range-text">{percFood}</p>
                {/if}
            </CardBody>
        </Card>
    {/if}
</main>

<style>
    h2{
        text-decoration-color: #57B95D;
    }
    input {
        accent-color: #57B95D;
    }
</style>