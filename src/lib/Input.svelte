<script lang="ts">
  import { OMDB_API_KEY } from '@/consts';
  import Movie from '@/lib/Movie.svelte';
  import type { OmdbAPIResponse, Search } from '@/types';

  let value = '';
  let response: Promise<Search[]> = Promise.resolve([]);

  const handleInput = (event: Event & { currentTarget: EventTarget & HTMLInputElement }) => {
    value = event.currentTarget.value;
  };

  $: if (value.length > 2) {
    response = fetch(`https://www.omdbapi.com/?s=${value}&type=movie&apikey=${OMDB_API_KEY}`)
      .then((res) => {
        if (!res.ok) throw new Error('Something bad happened with the fetching of movies');
        return res.json();
      })
      .then((apiResponse: OmdbAPIResponse) => apiResponse.Search || []);
  }
</script>

<input class="search-input" type="text" placeholder="Search" {value} on:input={handleInput} />

{#await response}
  <strong>Loading ...</strong>
{:then movies}
  <section class="movies">
    {#each movies as { Title, Poster, Year, Type }}
      <!-- {#if Type === 'movie'} -->
      <Movie title={Title} poster={Poster} year={Year} />
      <!-- {/if} -->
    {:else}
      <strong>No results</strong>
    {/each}
  </section>
{:catch error}
  <p>X There has been an error</p>
{/await}

<style>
  .search-input {
    border-radius: 0;
    border-bottom: 2px solid #575756;
    color: #575756;
    font-size: 17px;
    line-height: 18px;
    padding: 12px 10px;
    width: 80%;
    outline: 0;
    align-self: center;
    margin-bottom: 1rem;
  }

  .search-input::placeholder {
    color: rgba(87, 87, 86, 0.8);
    text-transform: uppercase;
    letter-spacing: 1.5px;
  }

  .movies {
    display: grid;
    gap: 20px;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    place-content: center;
    place-items: center;
  }
</style>
