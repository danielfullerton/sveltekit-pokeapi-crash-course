<script context="module" lang="ts">
  import { Pokemon } from '../../types/Pokemon';

  export async function load({ page }): Promise<{ props: { pokemon: Pokemon } }> {
    const id = page.params.id;
    const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
    const res = await fetch(url);
    const pokemon = await res.json();
    return { props: { pokemon } };
  }
</script>

<script lang="ts">
  export let pokemon: Pokemon;
</script>

<h1>
  {pokemon.name}
</h1>
