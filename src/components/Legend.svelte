<script>

</script>


<p id="legend-title">Filter by status <span class="no-bold">(click legend to filter):</span></p>
<ul id="legend">
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