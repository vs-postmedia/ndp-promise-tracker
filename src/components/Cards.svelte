<script>
    export let data = [];
    export let value = '';

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
</script>

<ul class="cards-container" bind:clientWidth={width}>
    {#each data as d}
        <li class="card {d.category} {d.category} {d.status ? d.status.toLowerCase() : ''}">
            <div class="card-title">
                <div class="color-bar {d.status}"></div>
                <h2>{d.title}</h2>
            </div>
            <p><span class="highlight">NDP claim:</span> {d.description}</p>
            <p class="notes">{d.notes_public}</p>
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
        border: 1px solid var(--grey04);
        border-radius: 5px;
        box-shadow: 3px 2px 7px var(--grey05);
        cursor: pointer;
        margin: 0.5rem 0.25rem;
        padding: 5px;
        width: 100%;
    }
    .card.hidden {
        display: none;
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

    .card p .highlight {
        font-family: 'BentonSansCond-Bold', sans-serif;
        font-weight: 800;
    }

    #app .card .notes {
        color: var(--grey03);
        font-family: 'BentonSansCond-RegItalic', italic;
    }

    .card .color-bar {
        background-color: var(--grey04);
        border-radius: 3px;
        margin-right: 10px;
        max-width: 10px;
        min-width: 10px;
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

    @media (min-width: 615px) {
        .card {
            width: 45%;
        }
    }
</style>