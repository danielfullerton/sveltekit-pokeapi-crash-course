<script context="module" lang="ts">
  import { Pokemon } from '../types/Pokemon';

  export async function load(): Promise<{ props: { pokemon: Pokemon } }> {
    const url = `https://pokeapi.co/api/v2/pokemon?limit=150`;
    const res = await fetch(url);
    const data = await res.json();
    const pokemon = data.results.map((data, index): Pokemon => {
      return {
        name: data.name,
        id: index + 1,
        image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index + 1}.png`
      };
    });
    return { props: { pokemon } };
  }
</script>

<script lang="ts">
  import PokemonCard from '../components/pokemonCard.svelte';
  export let pokemon: Pokemon[];

  let searchTerm = '';
  let filteredPokemon = [];

  $: {
    if (searchTerm) {
      filteredPokemon = pokemon.filter(p => p.name.toLowerCase().includes(searchTerm.toLowerCase()))
    } else {
      filteredPokemon = [...pokemon];
    }
  }
</script>

<svelte:head>
  <title>Svelte Kit Pokedex</title>
</svelte:head>
<h1>Svelte Kit Pokedex</h1>

<div>
  <input type="text" placeholder="Search Pokemon" bind:value={searchTerm}>
</div>

{#each filteredPokemon as p(p.id)}
  <PokemonCard pokemon={p} />
{/each}
