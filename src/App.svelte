<script>
    // COMPONENTS
    import { onMount } from 'svelte';
    import { csvParse } from 'd3-dsv';
    import Cards from "$components/Cards.svelte";
    import Topline from "$components/Topline.svelte";
    import { tidy, count, groupBy, summarize } from '@tidyjs/tidy';
    import Select from "svelte-select"; // https://github.com/rob-balfre/svelte-select

    

    // DATA
    import { menuItems } from "$data/menu-items";
    const dataUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vQFo5pVsIFo3uzc017mwdqjalrgYTANsPLEKyiqqvD7s07xJQazhJ3ooAQyFUDQwDMiXQCPdujR9C6l/pub?gid=111238127&single=true&output=csv';

    // VARIABLES
    let data, filteredData, value;
    const defaultSelectValue = menuItems[0].value;

    // REACTIVE VARIABLES
    $: value, updateData(value);

    async function fetchData(url) {
        const resp = await fetch(url);
        data = await resp.text();
        return csvParse(data);
    }

    async function processToplineData(data) {
        return tidy(
            data,
            groupBy(['status']),
            summarize({
                total: count('status')
            })
        )
    }

    function updateData(value) {
        if (!value || !value.value || value.value === 'all') return;

        console.log(value.value);
        console.log(data[0].category);

        filteredData = data.filter(d => d.category === value.value);

        console.log(data)
    }

    async function init() {
        // fetch remote data
        data = await fetchData(dataUrl);
        filteredData = data;
        // console.log(data);

        const toplineData = await processToplineData(data);
        console.log(toplineData)

        // default display selector value
		value = defaultSelectValue;
    }

    onMount(init);
</script>

<header>
    <h1>Tracking NDP election promises</h1>
    <p class="subhead">Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
</header>

<main>
    <Select items={menuItems}
        bind:value
        change={updateData}
        placeholder="Pick a category..."
		showChevron="true"
		listOpen={false}
    />

    <p id="legend-title">Status: </p>
    <ul id="legend">
        <!-- <li>
            <p class="bold">Status: </p>
        </li> -->
        <li>
            <div class="swatch unrated"></div>
            <p>Unrated</p>
        </li>
        <li>
            <div class="swatch unmet"></div>
            <p>Unmet</p>
        </li>
        <li>
            <div class="swatch in-progress"></div>
            <p>In progress</p>
        </li>
        <li>
            <div class="swatch partially-met"></div>
            <p>Partially met</p>
        </li>
        <li>
            <div class="swatch complete"></div>
            <p>Complete</p>
        </li>
    </ul>
    
    <Topline 
        data={data}
        value={value}
    />
    <Cards 
        data={filteredData}
    />
</main>

<footer>
    <p class="note">NOTE: tk.</p>
    <p class="source">Source:  <a href="https:vancouversun.com" target="_blank">TK</a></p>
</footer>
  
<style>
    @import '$css/normalize.css';
    @import '$css/fonts.css';
    @import '$css/colors.css';
    @import '$css/app.css';

    header {
		margin-bottom: 2rem;
	}
	header > h1 {
        line-height: 1.3;
		text-align: center;
	}
	header .subhead {
		margin: 0 auto;
		max-width: 525px;
		text-align: center;
	}

    /* LEGEND */
    #legend-title {
        font-family: 'BentonSansCond-Bold';
        font-weight: 800;
        margin: 25px 0 5px 0;
    }
    #legend {
        display: flex;
        flex-wrap: wrap;
        margin: 0 0 2rem 0;
    }

    #legend li {
        display: flex;
        margin: 5px 0;
    }
    #legend .swatch {
        background-color: lightgrey;
        border-radius: 3px;
        height: 15px;
        margin: 2px 5px 0 10px;
        width: 15px;
    }
    #legend .swatch.unmet {
        background-color: var(--red02);
    }
    #legend .swatch.complete {
        background-color: var(--green02);
    }
    #legend .swatch.partially-met {
        background-color: var(--yellow02);
    }
    #legend .swatch.in-progress {
        background-color: var(--orange02);
    }


    /* COMBOBOX SELECTOR */
  	:global(.svelte-select) {
		margin: 1rem auto !important;
		max-width: 250px;
  	}
  	:global(input:focus) {
		outline: none;
  	}

	:global(
		.svelte-select .selected-item,
		.svelte-select .item,
		.svelte-select input
	) {
		font-family: 'BentonSansCond-Regular', sans;
	}
</style>
