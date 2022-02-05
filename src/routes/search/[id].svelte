<script context="module">
    import { set_now } from "svelte/internal";
    import {fly} from 'svelte/transition'
    
    
        export async function load({fetch, params}) {
            const res = await fetch(
                `https://api.themoviedb.org/3/search/movie?api_key=${import.meta.env.VITE_API}&language=en-US&query=${params.id}&page=1&include_adult=true`
                );
            const data = await res.json();
            if (res.ok) {
                return {
                    props: { searchedMovie : data.results }
                };
            }
        }
</script>

<script>
    import MovieCard from "../../components/MovieCard.svelte";
    export let searchedMovie;
</script>

<div class="searched-movies" in:fly={{y: 50, duration: 500, delay: 500}} out:fly={{duration: 500}}>
    {#each searchedMovie as movie}
    <MovieCard {movie} />
    {/each}
</div>

<style>
    .searched-movies {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        grid-column-gap: 1rem;
        grid-row-gap: 2rem;
        height: 20vh;
    }
</style>