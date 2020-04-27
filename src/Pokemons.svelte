<script>
  import { onMount } from "svelte";
  import Pokemon from "./Pokemon.svelte";

  //will hold all the data
  let pokemons;
  let limit = 20;
  let offset = 0;
  let next;

  $: promise = fetch(
    "https://pokeapi.co/api/v2/pokemon?limit=" + limit + "&offset=" + offset
  )
    .then(r => r.json())
    .then(d => {
      pokemons = d;
      next = d.next;
    });

  function handleNext() {
    offset += 20;
    limit = offset > 131 ? 11 : 20;
  }

  function handlePrev() {
    limit = 20;
    offset -= 20;
  }
</script>

<style>
  ul {
    margin: 0;
    padding: 0;
    display: flex;
    flex-wrap: wrap;
  }

  ul li {
    flex: 1;
    list-style: none;
    padding: 1rem;
    min-width: 17rem;
    max-width: 17rem;
    transition: all 5s;
  }

  li.ctrl > div {
    background: #fbfbfb;
    text-align: center;
    max-width: 10rem;
  }
</style>

{#await promise}
  <h1>loading...</h1>
{:then pokeData}
  <ul>
    {#if offset > 0}
      <li class="ctrl ctrl-prev">
        <div on:click={handlePrev}>PREV</div>
      </li>
    {/if}
    {#each pokemons.results as poke}
      <li>
        <Pokemon {poke} />
      </li>
    {/each}
    {#if offset < 131}
      <li class="ctrl ctrl-next">
        <div on:click={handleNext}>NEXT</div>
      </li>
    {/if}
  </ul>
{/await}
