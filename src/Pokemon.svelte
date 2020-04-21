<script>
  import { onMount } from "svelte";
  import PokemonData from "./PokemonData.svelte";
  import PokemonTypes from "./PokemonTypes.svelte";

  export let poke;
  let pokeData;

  onMount(async () => {
    await fetch(poke.url)
      .then(r => r.json())
      .then(data => {
        pokeData = data;
      });
  });
</script>

<style>
  div.pokemon {
    display: flex;
    flex-direction: column;
    width: 100%;
    justify-content: center;
    border: 1px solid gainsboro;
    border-radius:2px;
  }

  div.pokemon > .header {
    text-align: center;
    padding: 0 1rem;
  }

  img.pokemon-image {
    width: 9rem;
    height: auto;
  }

  div.pokemon div.body {
    display:flex;
    flex-direction: column;
    align-items: center;
    padding: 1rem;
    border-top: 1px solid gainsboro;

  }
</style>

{#if pokeData}
  <div class="pokemon">
    <div class="header">
      <h1>{poke.name.toUpperCase()}</h1>
      <PokemonTypes types={pokeData.types.sort((a,b) => (a.slot > b.slot) ? 1 : ((b.slot > a.slot) ? -1 : 0))} />
    </div>
    <div class="body">
      <!-- component for stats -->
      <img
        class="pokemon-image"
        src="https://pokeres.bastionbot.org/images/pokemon/{pokeData.id}.png"
        alt="{poke.name.toUpperCase()} image" />
    </div>
  </div>
{:else}
  <p class="loading">loading...</p>
{/if}
