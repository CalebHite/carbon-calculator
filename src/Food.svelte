<script>
    let isVeg = false;
    let veg;
    let foodOptions = [
        {
            id: "food0",
            name: "Beef",
            isChecked: false
        },
        {
            id: "food1",
            name: "Dairy",
            isChecked: false
        },
        {
            id: "food2",
            name: "Pork",
            isChecked: false
        },
        {
            id: "food3",
            name: "Poultry",
            isChecked: false
        },
        {
            id: "food4",
            name: "Eggs",
            isChecked: false
        },
        {
            id: "food5",
            name: "Legumes/Vegetables/Fruits",
            isChecked: false
        },
    ];
    var foods = [];
</script>

<main>
    <h2>Food</h2>
    <h3>Are you Vegetarian or Vegan?</h3>
    <label for="vegYes">Yes</label>
    <input type="radio" id="vegYes" name="isVeg" value="yes" on:click={() => {
        isVeg = true;
    }}>
    <label for="vegNo">No</label>
    <input type="radio" id="vegNo" name="isVeg" value="no" on:click={() => {
        isVeg = false;
    }}>
    {#if isVeg === true}
        <label for="vegetarian">Vegetarian</label>
        <input type="radio" id="vegetarian" name="veg" value="vegetarian" on:click={() => {
            veg = "vegetarian";
        }}>
        <label for="vegan">Vegan</label>
        <input type="radio" id="vegan" name="veg" value="vegan" on:click={() => {
            veg = "vegan";
        }}>
    {/if}
    <h3>Which of These Foods Do You Eat Often?</h3>
    
    
    {#each foodOptions as {id, name, isChecked}}
        <label for={id}>{name}</label><br>
        <input type="checkbox" id={id} name={name} bind:checked={isChecked} on:click={() => {
            if(isChecked === false){
                foods.push(name);
            }
            else{
                foods = foods.filter((e) => { return e !== name })
            }
        }}>
    {/each}

</main>

<style>

</style>