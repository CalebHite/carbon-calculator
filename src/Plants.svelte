<script>
    let hasTrees = false;
    let trees;
    let hasGarden;
    let percFood;

    export var amounts;
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
    }}>
    {#if hasTrees === true}
        <h3>How Many?</h3>
        <input type="range" id="trees" name="trees" min="1" max="200" bind:value={trees}>
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
    }}>
    {#if hasGarden === true}
        <h3>What Percent of Your Food Do You Grow?</h3>
        <input type="range" id="percFood" name="percFood" min="1" max="100" bind:value={percFood}>
        {#if percFood != undefined}
            <p>{percFood}</p>
        {/if}
    {/if}
</main>

<style>

</style>