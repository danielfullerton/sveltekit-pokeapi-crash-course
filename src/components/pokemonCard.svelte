<script lang="ts">
  import { Pokemon } from '../types/Pokemon';
  import { fly } from 'svelte/transition';

  export let pokemon: Pokemon;
</script>

<a transition:fly href={`/pokemon/${pokemon.id}`}>
  <img src={pokemon.image} alt={pokemon.name}>
  <h2>{pokemon.id}. {pokemon.name}</h2>
</a>
