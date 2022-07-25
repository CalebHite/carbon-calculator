<script>
    import { items } from "./stores.js";

    let foods = [
        {
            type: "food",
            id: "food0",
            name: "Beef",
            isChecked: false,
            value: 804.22
        },
        {
            type: "food",
            id: "food1",
            name: "Dairy",
            isChecked: false,
            value: 298.08
        },
        {
            type: "food",
            id: "food2",
            name: "Pork",
            isChecked: false,
            value: 209.27
        },
        {
            type: "food",
            id: "food3",
            name: "Poultry",
            isChecked: false,
            value: 153.3
        },
        {
            type: "food",
            id: "food4",
            name: "Eggs",
            isChecked: false,
            value: 108.28
        },
        {
            type: "food",
            id: "food5",
            name: "Legumes/Vegetables/Fruits",
            isChecked: false,
            value: 337.625
        },
    ];
</script>

<main>
    <h2>Food</h2>
    <h3>Which of These Foods Do You Eat Often?</h3>
    <div class="options">
        {#each foods as {id, name, isChecked}, i}
        <div class="input">
            <label for={id}>{name}</label><br>
            <input type="checkbox" id={id} name={name} bind:checked={isChecked} on:click={() => {
                if(isChecked === false){
                    $items = [...$items, foods[i]];
                }
                else{
                    $items = $items.filter((e) => { return e.name !== name});
                }
            }}>
        </div>
    {/each}
    </div>
</main>

<style>
    h2{
        text-decoration-color: #FFB04A;
    }
</style>