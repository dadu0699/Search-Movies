<script>
    import Movie from "./Movie.svelte";

    let value = "";
    let response = [];

    const handleInput = (event) => (value = event.target.value);

    $: if (value.length > 2) {
        response = fetch(`https://www.omdbapi.com/?s=${value}&apikey=7d354b84`)
            .then((res) => {
                if (!res.ok) {
                    throw new Error(
                        "Something bad happened with the fetching of movies"
                    );
                } else {
                    return res;
                }
            })
            .then((res) => res.json())
            .then((apiResponse) => apiResponse.Search || []);
    }
</script>

<input placeholder="Search movies ..." {value} on:input={handleInput} />

{#await response}
    <strong>Loading ...</strong>
{:then movies}
    {#each movies as { Title, Poster, Year, Type }}
        {#if Type === "movie"}
            <Movie title={Title} poster={Poster} year={Year} />
        {/if}
    {:else}
        <strong>No results</strong>
    {/each}
{:catch error}
    <p>X There has been an error</p>
{/await}
