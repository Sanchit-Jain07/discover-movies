<script>
    import Movie from './Movie.svelte'
    import API_KEY from './apikey.js'

    const poster_base_url = 'https://image.tmdb.org/t/p/w500'

    export let genre
    export let type
    export let region
    export let language

    async function get_movies(type, region, language) {
        const query_string = type==='genre' ? `https://api.themoviedb.org/3/discover/movie?api_key=${API_KEY}&with_genres=${genre.id}&include_adult=false&sort_by=popularity.desc&region=${region}&with_original_language=${language}` : `https://api.themoviedb.org/3/trending/movie/day?api_key=${API_KEY}`
        const res = await fetch(query_string)
        const result = await res.json()

        if (res.ok) {
            let movie_list = []
            result['results'].forEach(movie => {
                movie_list.push({
                    name: movie.original_title,
                    desc: movie.overview,
                    poster: poster_base_url + movie.poster_path,
                })
            })
            return movie_list
        } 
    }

    $: promise = get_movies(type, region, language)

    export let design_type
    let bg_color = design_type === 0 ? '#fff' : '#000'
    let color = design_type === 0 ? '#000' : '#fff'
    let flex_direction = design_type === 0 ? 'row' : 'row-reverse'

</script>

<div class="container" style="--bg-color: {bg_color}; --text-color: {color}; --flex-d: {flex_direction}">
    {#if design_type === 0}
        <div class="genre">
            {genre.name}
        </div>
    {/if}
    {#await promise}
        <div class="movies loading">
            <div class="loader"></div>
        </div>
    {:then data}
        <div class="movies">
            {#each data as movie}
                <Movie name={movie.name} desc={movie.desc} poster={movie.poster} scroll_snap={design_type}/>
            {/each}
        </div>
    {/await}
    
    {#if design_type === 1}
        <div class="genre">
            {genre.name}
        </div>
    {/if}
</div>

<style>
    .container {
        display: flex;
        width: 100vw;
        height: 70vh;
        background-color: var(--bg-color);
        scroll-snap-align: start;
    }
    .genre {
        width: 30%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        font-family: 'Montserrat', sans-serif;
        color: var(--text-color);
        font-size: 60px;
    }
    .movies {
        width: 70%;
        height: 100%;
        display: flex;
        flex-direction: var(--flex-d);
        align-items: center;
        overflow-x: scroll;
        scroll-snap-type: x mandatory;
    }

    .loading {
        justify-content: center;
    }

    .loader {
        border: 16px solid #f3f3f3; 
        border-top: 16px solid #3498db; 
        border-radius: 50%;
        width: 120px;
        height: 120px;
        animation: spin 2s linear infinite;
    }

    @keyframes spin {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
    }

    ::-webkit-scrollbar {
        height: 10px;
    }

    ::-webkit-scrollbar-track {
        background: var(--bg-color);
    }

    ::-webkit-scrollbar-thumb {
        background: var(--text-color);
        border-radius: 10px;
    }

    ::-webkit-scrollbar-thumb:hover {
        background: #333;
    }

</style>