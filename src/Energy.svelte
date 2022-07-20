<script>
    let residence;
    let people;
    let hasPanels = false;
    let solarPanels;

    export var amounts;
</script>

<main>
    <h2>Energy</h2>
    <h3>Place of Residence</h3>
    <label for="house">House</label>
    <input type="radio" id="house" name="residence-type" value="house" on:click={() => {
        residence = "house";
    }}>
    <label for="mobile-home">Mobile Home</label>
    <input type="radio" id="mobile-home" name="residence-type" value="mobile-home" on:click={() => {
        residence = "mobile-home";;
    }}>
    <label for="apartmentSmall">Apartment With 2-4 Units</label>
    <input type="radio" id="apartmentSmall" name="residence-type" value="apartmentSmall" on:click={() => {
        residence = "apartmentSmall";
    }}>
    <label for="apartmentLarge">Apartment With 5+ Units</label>
    <input type="radio" id="apartmentLarge" name="residence-type" value="apartmentLarge" on:click={() => {
        residence = "apartmentLarge";
    }}>
    <h3>How Many People Live in Your Residence?</h3>
    <input type="range" id="residence" name="residence" min="1" max="10" bind:value={people}>
    {#if people != undefined}
        <p>{people}</p>
    {/if}
    <h3>Do You Own Solar Panels?</h3>
    <label for="hasPanels">Yes</label>
    <input type="radio" id="panelsYes" name="hasPanels" value="yes" on:click={() => {
        hasPanels = true;
    }}>
    <label for="hasPanels">No</label>
    <input type="radio" id="panelsNo" name="hasPanels" value="no" on:click={() => {
        hasPanels = false;
    }}>
    {#if hasPanels === true}
        <h3>What Percentage of Your Power is Produced by Your Solar Panels?</h3>
        <input type="range" id="solar-panels" name="solar-panels" min="1" max="100" bind:value={solarPanels}>
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