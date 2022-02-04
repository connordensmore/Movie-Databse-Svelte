<script context="module">
import { set_now } from "svelte/internal";


    export async function load({fetch}) {
        const res = await fetch(
            `https://api.themoviedb.org/3/movie/popular?api_key=26c997e52224acc512b6eab806cf31ad&language=en-US&page=1`
            );
        const data = await res.json();
        if (res.ok) {
            return {
                props: { popular : data.results }
            };
        }
    }
</script>

<script>
    import PopularMovies from '../components/PopularMovies.svelte';
    export let popular;
</script>


<section>
    <PopularMovies {popular} />
</section>