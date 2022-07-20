<script>
    let hasTrees = false;
    let hasGarden = false;
    let percFood;
    let trees;

    var plantItems = [];
</script>

<main>
    <h2>Plants</h2>
    <h3>Do You Have Trees on Your Property?</h3>
    <label for="hasTrees">Yes</label>
    <input type="radio" id="treesYes" name="hasTrees" value="yes" on:click={() => {
        hasTrees = true;
    }}>
    <label for="hasTrees">No</label>
    <input type="radio" id="treesNo" name="hasTrees" value="no" on:click={() => {
        hasTrees = false;
        plantItems = plantItems.filter((e) => { return e.type !== "trees" });
        plantItems.push({
            type: "trees",
            name: "Trees",
            id: "trees",
            value: 0
        })
    }}>
    
    {#if hasTrees === true}
        <h3>How Many?</h3>
        <input type="range" id="trees" name="trees" min="1" max="200" bind:value={trees} on:click={()=>{
            plantItems = plantItems.filter((e) => { return e.type !== "trees" });
            plantItems.push({
                type: "trees",
                name: "Trees",
                id: "trees",
                value: (trees * -1)
            })
        }}>

        {#if trees != undefined}
            <p>{trees}</p>
        {/if}
    {/if}
    <h3>Do You Own a Garden?</h3>
    <label for="hasGarden">Yes</label>
    <input type="radio" id="gardenYes" name="hasGarden" value="yes" on:click={() => {
        hasGarden = true;
    }}>
    <label for="hasGarden">No</label>
    <input type="radio" id="gardenYes" name="hasGarden" value="no" on:click={() => {
        hasGarden = false;
        plantItems = plantItems.filter((e) => { return e.type !== "garden" });
        plantItems.push({
            type: "garden",
            name: "Garden",
            id: "garden",
            value: 0
        })
    }}>
    {#if hasGarden === true}
        <h3>What Percent of Your Food Do You Grow?</h3>
        <input type="range" id="percFood" name="percFood" min="1" max="100" bind:value={percFood} on:click={()=>{

            plantItems = plantItems.filter((e) => { return e.type !== "garden" });
            plantItems.push({
                type: "garden",
                name: "Garden",
                id: "garden",
                value: (( percFood / 100 ) * -1)
            })
        }}>
        {#if percFood != undefined}
            <p>{percFood}</p>
        {/if}
    {/if}
</main>

<style>
    h2{
        text-decoration-color: #57B95D;
    }
</style>