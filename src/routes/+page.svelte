<script>
    let choices = [{text: "Velg film: ", input: false, value: "Kampen om Narvik"}, 
    {text: "Antall: ", input: true, value: ""},
    {text: "Fornavn: ", input: true, value: ""},
    {text: "Etternavn: ", input: true, value: ""},
    {text: "Telefonnr: ", input: true, value: ""},
    {text: "Epost: ", input: true, value: ""}]
    let filmer = ["Kampen om Narvik", "Babylon","Avatar: The Way of Water","A Man Called Otto"]
    let billetter = []
    function kjøpbillett(){
        for(let choice of choices){
            if(!choice.value){
                return
            }}
        let copy = JSON.parse(JSON.stringify(choices))
        billetter = [...billetter, copy]
    }
    function slettbillett(){
        billetter = []
    }
</script>
<h1>Bestilling av Kinobilletter</h1>
{#each choices as choice}
<div>
    <label for="{choice.text}">{choice.text}</label>
    {#if choice.input}
        <input id="{choice.text}" bind:value={choice.value}/>
        {#if !choice.value}
            <label for="{choice.text}" id="error">Field cannot be empty</label>
        {/if}
    {:else}
        <select bind:value={choice.value}>
            {#each filmer as film}
            <option value="{film}">{film}</option>
            {/each}
        </select>    
    {/if}
</div>
{/each}
<button on:click="{kjøpbillett}">Kjøp billett</button>
<h2>Alle billetter</h2>
<table id="table">
    <tr>
        <th>Film</th>
        <th>Antall</th>
        <th>Fornavn</th>
        <th>Etternavn</th>
        <th>TelefonNr</th>
        <th>Epost</th>
    </tr>
    {#each billetter as billett}
    <tr>
        {#each billett as ting}
        <th contenteditable="true" bind:innerHTML={ting.value}></th>
        {/each}
    </tr>
    {/each}
</table>
<button on:click={slettbillett}>Slett billetter</button>

<style>
#error{
    color:red;
}
table{
    width: 100%;
    text-align: center;
}
</style>
