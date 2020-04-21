<script>
  import { onMount } from "svelte";
  import PokemonTypes from "./PokemonTypes.svelte";

  export let url;

  let pokeData;

  onMount(async () => {
    await fetch(url)
      .then(r => r.json())
      .then(data => {
        pokeData = data;
      });
  });
</script>

<style>
  img.pokemon-img {
    width: 3rem;
    height: auto;
    margin-bottom: 1rem;
  }

  ul.stats {
    list-style: none;
    padding: 0;
    display: flex;
  }

  ul.stats li {
    flex: 1 0 0;
  }
</style>

{#if pokeData}
  <img
    class="pokemon-img"
    alt={pokeData.name.toUpperCase()}
    src="https://pokeres.bastionbot.org/images/pokemon/{pokeData.id}.png" />

  <PokemonTypes types={pokeData.types} />

  <ul class="stats">
    {#each pokeData.stats as stat}
      <li class="stat-info">
        <h4>{stat.stat.name.toUpperCase()}</h4>
        <p>Base: {stat.base_stat}</p>
      </li>
    {/each}
  </ul>
{:else}
  <p class="loading">loading...</p>
{/if}
