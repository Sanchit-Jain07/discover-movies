<script>
    export let name
    export let poster
    export let desc
    export let scroll_snap
    let color = scroll_snap === 0 ? '#000' : '#fff'
    scroll_snap = scroll_snap === 0 ? 'start' : 'end'
    let description_div = ''
    const animate = () => {
        description_div = description_div==='hide' ? '' : 'hide'
    }
</script>

<div class="card" style="scroll-snap-align: {scroll_snap}">
    <img src="{poster}" alt="{name}" class="poster" on:mouseenter={animate} on:mouseleave={animate} style="color: {color}">
    <div class="desc {description_div}" on:mouseenter={animate} on:mouseleave={animate}>
        <h2>{name}</h2>
        {desc}
    </div>
</div>

<style>
    .card {
        width: 220px;
        height: 300px;
        margin: 20px;
        margin-top: 0;
        position: relative;
        overflow-y: hidden;
        min-width: 220px;
        scroll-snap-stop: always;
    }
    .poster {
        width: 100%;
        height: 100%;
    }
    .name {
        font-size: 20px;
        font-family: 'Montserrat', sans-serif;
        font-weight: bold;
        color: red;
    }
    .desc {
        font-family: 'Montserrat', sans-serif;
        font-weight: bold;
        background: rgba(255,255,255,0.9);
        width: 100%;
        height: 100%;
        position: absolute;
        top: 100%;
        box-sizing: border-box;
        padding: 10px;
        transition: top 1s ease;
        overflow-y: auto;
    }
    .hide {
        top: 0;
    }
    ::-webkit-scrollbar {
        width: 10px;
    }

    ::-webkit-scrollbar-track {
        background: #fff;
    }

    ::-webkit-scrollbar-thumb {
        background: #485459;
        border-radius: 10px;
    }

    ::-webkit-scrollbar-thumb:hover {
        background: #333;
    }
</style>
