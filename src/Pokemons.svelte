<script>
  import { onMount } from "svelte";
  import Pokemon from "./Pokemon.svelte";

  //will hold all the data
  let pokemons;

  onMount(async () => {
    await fetch("https://pokeapi.co/api/v2/pokemon?&offset=0")
      .then(r => r.json())
      .then(data => {
        console.log(data);
        pokemons = data.results;
      });
  });
</script>

<style>
  ul {
    margin: 0;
    padding: 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
    align-content: space-evenly;
  }

  ul li {
    flex: 1;
    list-style: none;
    padding: 1rem;
    min-width: 17rem;
    max-width: 17rem;
  }
</style>

{#if pokemons}

  <ul>
    {#each pokemons as poke}
      <li>
        <Pokemon {poke} />
      </li>
    {/each}
  </ul>
{:else}
  <p class="loading">loading...</p>
{/if}
