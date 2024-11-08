<script>
    export let data = [];
    export let value = '';

    // LIBS
    import { onMount } from 'svelte';

    // VARS
    let tooltipData;
    let width = 500;
    let height = 500;

    const margin = {
		top: 20,
		right: 20,
		bottom: 20,
		left: 20 
	};
    // $: console.log(data);

    // FUNCTIONS
    function init() {
        console.log('TOPLINE INIT!')
    }
    function addCommasToNumber(number) {
        return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }

    // LIGHTS! CAMERA! ACTION!
    onMount(init);
</script>


<!-- <pre>CHART: Combobox value = {JSON.stringify(value) || 'No selection'}</pre> -->

<ul class="cards-container" bind:clientWidth={width}>
    {#each data as d}
        <li class="card {d.category} {d.category} {d.status ? d.status.toLowerCase() : ''}">
            <div class="card-title">
                <div class="color-bar {d.status}"></div>
                <h2>{d.title}</h2>
            </div>
            <p>{d.description}</p>
            <p class="notes">{d.notes}</p>
        </li>
    {/each}
</ul>

<style>
    .cards-container {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
    }
    .card {
        margin: 0.5rem 0.25rem;
        cursor: pointer;
        width: 100%;
    }
    .card .card-title {
        display: flex;
    }
    .card h2 {
        font-size: 1.25rem;
        line-height: 1.3;

    }
    .card p {
        margin-top: 10px;
    }

    .card .notes {
        color: var(--grey03);
        font-family: 'BentonSansCond-RegItalic', italic;
    }

    .card .color-bar {
        background-color: var(--grey04);
        border-radius: 3px;
        margin-right: 10px;
        width: 10px;
    }
    .card .color-bar.unmet {
        background-color: var(--red02);
    }
    .card .color-bar.complete {
        background-color: var(--green02);
    }
    .card .color-bar.partially-met {
        background-color: var(--yellow02);
    }
    .card .color-bar.in-progress {
        background-color: var(--orange02);
    }

    @media (min-width: 550px) {
        .card {
            width: 48%;
        }
        .card .color-bar {
            margin-right: 15px;
            width: 20px;
        }
    }
</style>