<script>
    import Movie from './Movie.svelte'
    import Genre from './Genre.svelte'
    import genres from './genres.js'

    let region = 'US'
    let language = 'en'
    let us, ind, en, hi
    us = en = 'active'
    const setRegion = (reg) => {
        region = reg
        if (reg === 'US') {
            us = 'active'
            ind = ''
        } else {
            ind = 'active'
            us = ''
        }
    }
    const setLang = (lang) => {
        language = lang
        if (lang === 'en') {
            en = 'active'
            hi = ''
        } else {
            hi = 'active'
            en = ''
        }
    }
</script>

<div class="select">
    <div class="region">
        <div class="heading">
            Select Region
        </div>
        <div class="btns">
            <button id="us" class="btn {us}" on:click={() => {setRegion('US')}}>
                United States of America
            </button>
            <button id="in" class="btn {ind}" on:click={() => {setRegion('IN')}}>
                India
            </button>
        </div>
    </div>
    <div class="language">
        <div class="heading">
            Select Language
        </div>
        <div class="btns">
            <button id="en" class="btn {en}" on:click={() => {setLang('en')}} >
                English
            </button>
            <button id="hi" class="btn {hi}" on:click={() => {setLang('hi')}}>
                Hindi
            </button>
        </div>
    </div>
</div>

<Genre design_type={0} genre={{name: 'Trending'}} type={'trending'} {region} {language}/>
{#each genres as genre,i}
<Genre design_type={(i+1)%2} {genre} type={'genre'} {region} {language}/>
{/each}

<style>
    .select {
        display: flex;
    }
    .region,.language {
        width: 50vw;
        height: 20vh;   
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        align-items: center;
    }
    .btn {
        outline: none;
        background: #000;
        border-radius: 10px;
        padding: 10px;
        width: 40%;
        color: white;
        font-family: 'Montserrat', sans-serif;
        font-size: 16px;
        border: none;
        transform: scale(1);
        transition: transform 0.5s ease, border 0.1s ease;
    }
    .btns {
        display: flex;
        width: 100%;
        justify-content: space-around;
    }
    .heading {
        font-family: 'Montserrat', sans-serif;
        font-weight: bold;
        font-size: 32px;
    }
    .btn:hover {
        cursor: pointer;
        border: 5px solid cyan;
    }
    .btn:active {
        outline: none;
    }
    .btn.active {
        border: 5px solid cyan;
        transform: scale(1.1);
        pointer-events: none;
        cursor: not-allowed;
    }
</style>