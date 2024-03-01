<script>
    import { getContext, onMount } from "svelte";
    import lookbackData from "$data/lookback.csv";
    import { selectAll }from "d3-selection";
    import Book from "$components/Wall.Book.svelte";
    import Shelf from "$components/Wall.Shelf.svelte";
    import Prose from "$components/Prose.svelte";
    import SmallMultiples from "$components/SmallMultiples.svelte";

    export let bookMin;

    const copy = getContext("copy");

    let lookbackDoc;
    let lookbackClinch;
    let lookbackTravel;
    let smallChartRaunchiness;
    let smallChartIllustration;
    let smallChartRace;
    let introText;

    onMount(() => {
		lookbackDoc = selectAll(".lookback-doc");
        lookbackClinch = selectAll(".lookback-clinch");
        lookbackTravel = selectAll(".lookback-travel");
        smallChartRaunchiness = selectAll(".small-chart-raunchiness");
        smallChartIllustration = selectAll(".small-chart-illustration");
        smallChartRace = selectAll(".small-chart-race");
    })

    $: if (lookbackDoc !== undefined && lookbackTravel !== undefined && lookbackClinch !== undefined) {
        lookbackDoc
            .on("mouseover", function() {
                selectAll("#lookback .img-wrapper").classed("highlight", false);
                selectAll("#book_0 .img-wrapper, #book_1 .img-wrapper, #book_2 .img-wrapper").classed("highlight", true);
            })
            .on("mouseout", function() {
                selectAll("#lookback .img-wrapper").classed("highlight", false);
            })
        lookbackTravel
            .on("mouseover", function() {
                selectAll("#lookback .img-wrapper").classed("highlight", false);
                selectAll("#book_2 .img-wrapper").classed("highlight", true);
            })
            .on("mouseout", function() {
                selectAll("#lookback .img-wrapper").classed("highlight", false);
            })
        lookbackClinch
            .on("mouseover", function() {
                selectAll("#lookback .img-wrapper").classed("highlight", false);
                selectAll("#book_3 .img-wrapper, #book_4 .img-wrapper").classed("highlight", true);
            })
            .on("mouseout", function() {
                selectAll("#lookback .img-wrapper").classed("highlight", false);
            })

    }

    $: if (smallChartRaunchiness !== undefined && smallChartIllustration !== undefined && smallChartRace !== undefined) {
        smallChartRaunchiness
            .on("mouseover", function() {
                selectAll(".top-wrapper.illustration, .top-wrapper.race").style("opacity", 0.25);
            })
            .on("mouseout", function() {
                selectAll(".top-wrapper").style("opacity", 1);
            })
        smallChartIllustration
            .on("mouseover", function() {
                selectAll(".top-wrapper.raunchiness, .top-wrapper.race").style("opacity", 0.25);
            })
            .on("mouseout", function() {
                selectAll(".top-wrapper").style("opacity", 1);
            })
        smallChartRace
            .on("mouseover", function() {
                selectAll(".top-wrapper.illustration, .top-wrapper.raunchiness").style("opacity", 0.25);
            })
            .on("mouseout", function() {
                selectAll(".top-wrapper").style("opacity", 1);
            })
    }

    function setText() {
        if (copy !== undefined) {
			if (bookMin > 900) { introText = undefined; }
            else if (bookMin > 780) { introText = copy.lookBackOverflow_750; } 
            else if (bookMin > 740) { introText = copy.lookBackOverflow_650; }
            else if (bookMin > 680) { introText = copy.lookBackOverflow_600; }
            else { introText = copy.lookBackOverflow_else; }
		}
    }

    $: bookMin, setText();
</script>

<section id="lookback">
    <p class="prose">Produzido pelo <a href="https://www.dados.rio/" target="_blank" class="custom-link">Escritório de Dados</a> da Prefeitura da Cidade do Rio de Janeiro</p>
    <Prose copy={copy.lookBackA}/>
</section>

<style>
    .custom-link {
    color: inherit; /* Faz o link ter a mesma cor que o texto ao redor */
    text-decoration: underline; /* Remove o sublinhado do link */
}

     .prose {
        padding-bottom: 5rem;
        max-width: 42rem;
        margin: 0 auto;
        line-height: 2;
        padding: 4rem 1rem;
        font-weight: 500;
        font-size: var(--16px);
    }

    @media (max-width: 640px) {
        .prose {
            margin-top: 5rem;
            max-width: 24rem;
            margin-left:2rem;
        }
    }

   
    :global(#lookback a) {
		/* background-image: linear-gradient(180deg,transparent 0,var(--romance-pink-light) 0); */
	}
    :global(.books-fabio .marker) {
        display: none;
    }
   
    h5 {
        max-width: 40rem;
        text-transform: uppercase;
        margin: 4rem auto 2rem auto;
        font-family: var(--sans-display);
        font-weight: 900;
        text-align: center;
        padding: 0 1rem;
        font-size: var(--16px);
    }
    .book-wrapper {
        display: flex;
        flex-direction: row;
        max-width: 50rem;
        margin: -3rem auto 6rem auto;
        flex-wrap: wrap;
    }
    .shelves {
        height: auto;
        position: absolute;
        z-index: 1;
        display: flex;
        margin: 10px;
    }
    .books {
        height: auto;
        position: absolute;
        z-index: 1000;
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
    }
    .highlightBook {
        display: flex;
        justify-content: center;
        width: 33%;
        margin: auto;
        height: 10rem;
        z-index: 1;
    }
    :global(#lookback .book) {
        margin: 0.5rem 0 0 0.25rem;
        transition: 0.125s all linear;
    }
    :global(#lookback .img-wrapper.highlight) {
        transform: scale(1.25) translate(0, -15%);
        transition: 0.125s all linear;
    }
    :global(#lookback .lookback-doc, #lookback .lookback-clinch, #lookback .lookback-travel, #lookback .small-chart-raunchiness, #lookback .small-chart-illustration, #lookback .small-chart-race) {
        transition: 0.125s all linear;
        background-color: white;
        border-radius: 0.25rem;
        padding: 0.125rem 0.5rem;
        box-shadow: -2px 2px 5px  rgba(0,0,0,0.125);
        opacity: 1; 
        font-family: var(--sans-display);
        -ms-box-decoration-break: clone;
        -webkit-box-decoration-break: clone;
        -o-box-decoration-break: clone;
        box-decoration-break: clone;
    }
    :global(#lookback .lookback-doc, #lookback .lookback-clinch, #lookback .lookback-travel) {
        border: 2px solid var(--romance-pink)
    }
    :global(#lookback .lookback-doc:hover, #lookback .lookback-clinch:hover, #lookback .lookback-travel:hover, #lookback .small-chart-raunchiness:hover, #lookback .small-chart-illustration:hover, #lookback .small-chart-race:hover) {
        background-color: var(--romance-pink-light);
    }
    :global(#lookback .small-chart-raunchiness) {
        border: 2px solid var(--romance-blue);
    }
    :global(#lookback .small-chart-illustration) {
        border: 2px solid var(--romance-yellow);
    }
    :global(#lookback .small-chart-race) {
        border: 2px solid var(--romance-teal);
    }
    :global(#lookback .small-chart-raunchiness:hover) {
        background-color: var(--romance-blue-light);
    }
    :global(#lookback .small-chart-illustration:hover) {
        background-color: var(--romance-yellow-light);
    }
    :global(#lookback .small-chart-race:hover) {
        background-color: var(--romance-teal-light);
    }

    @media only screen and (min-width: 600px) {
        .book-wrapper {
            flex-wrap: nowrap;
        }
        .highlightBook {
            width: 30rem;
        }
        :global(#lookback .img-wrapper.highlight) {
            transform: scale(1.25) translate(0, 0);
            transition: 0.125s all linear;
        }
	}
</style>