<script>
    export let types;
</script>

<ul class="type-list">
    {#each types as type}
        <li>{type.type.name}</li>
    {/each}
</ul>

<style>
ul.type-list {
    padding: 0;
    margin:1rem 0;
    display:flex;
    align-items: center;
    justify-content: center;
    width:100%;
}

ul.type-list li {
    list-style: none;
    flex: 0 1 5rem;
    padding:3px;
    background-color: #efefef;
    text-align:center;
    margin-right: 0.5rem;
}

ul.type-list li:last-child {
    margin-right:0;
}
</style>
