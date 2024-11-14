<script>
    import { onMount } from 'svelte';

    function init() {
        // assign click event handler to legend items
        const liEls = document.querySelectorAll('#legend > li');
        liEls.forEach(li => li.addEventListener('click', legendClickEvent));
    }

    function legendClickEvent(e) {
        // console.log(e.currentTarget.className)
        const status = e.currentTarget.className.split(' ')[0];
        console.log(status)

        // filter cards by currentClass
        const cards = document.querySelectorAll('.card');

        // destructure cards (a NodeList) into an array & filter by current status
        const visibleCards = [...cards].filter(card => !card.className.includes(status));

        // remove hidden class from any card it's been applied to
        cards.forEach(card => card.classList.remove('hidden'));

        if (status !== 'all') {
            // add  hidden class to currently selected status
            visibleCards.forEach(card => card.classList.add('hidden'));
        }
    }


    // kick isht off
    onMount(init);
</script>


<p id="legend-title">Filter by status <span class="no-bold">(click legend to filter):</span></p>
<ul id="legend">
    <li class="all">
        <div class="all">☑️</div>
        <p>Show all</p>
    </li>
    <li class="unrated">
        <div class="swatch unrated"></div>
        <p>Unrated</p>
    </li>
    <li class="unmet">
        <div class="swatch unmet"></div>
        <p>Unmet</p>
    </li>
    <li class="in-progress">
        <div class="swatch in-progress"></div>
        <p>In progress</p>
    </li>
    <li class="partially-met">
        <div class="swatch partially-met"></div>
        <p>Partially met</p>
    </li>
    <li class="complete">
        <div class="swatch complete"></div>
        <p>Complete</p>
    </li>
</ul>

<style>
    /* LEGEND */
    #legend-title {
        font-family: 'BentonSansCond-Bold';
        font-weight: 800;
        margin: 25px 0 5px 0;
    }
    #legend-title .no-bold {
        font-family: 'BentonSansCond-Regular';
        font-weight: 400;
    }
    #legend {
        display: flex;
        flex-wrap: wrap;
        margin: 0 0 2rem 0;
    }

    #legend li {
        cursor: pointer;
        display: flex;
        margin: 5px 0;
    }
    #legend .swatch {
        background-color: var(--grey04);
        border-radius: 3px;
        height: 15px;
        margin: 2px 5px 0 10px;
        width: 15px;
    }
    #legend div.all {
        font-size: 1.25rem;
        padding: 1px 4px 0 0;
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
</style>