<script>
	import { getContext, onMount } from "svelte";
	import { activeSection, readingListVisible, xShiftRaunch, xShiftIllo, xShiftRace } from "$stores/misc.js";
	import { fly } from 'svelte/transition';
	import data from "$data/listings.csv";
    import { groups, ascending } from "d3-array";
	import { select } from "d3-selection";
	import ChapterMarker from "$components/ChapterMarker.svelte";
	import Chapter from "$components/Chapter.svelte";
	import BarChart from "$components/BarChart.svelte";
	import IntroScrolly from "$components/IntroScrolly.svelte";
	import ReadingList from "$components/ReadingList.svelte";
	import Lookback from "$components/Lookback.svelte";
	import Outro from "$components/Outro.svelte";
	import Footer from "$components/Footer.svelte";

	const copy = getContext("copy");
	
	let scrollY = 0;
	let w;
	let h;
	let body;
	let raunchinessData = data.filter(d => d.cover_url.includes("http")).filter(d => d["Man partially unclothed"] == "TRUE" || d["Woman partially unclothed"] == "TRUE").sort((a, b) => ascending(a["Year Season"], b["Year Season"]));
	let illustrationData = data.filter(d => d.cover_url.includes("http")).filter(d => d.Style == "Illustrated").sort((a, b) => ascending(a["Year Season"], b["Year Season"]));
	let raceData = data.filter(d => d.cover_url.includes("http")).filter(d => d["Has POC"] == "TRUE").sort((a, b) => ascending(a["Year Season"], b["Year Season"]));
	let yearTotals = groups(data, d => d.year);
	let barData = raunchinessData;
	let barColorHighlight = "#4C7DFE";
	let barColor = "#7da1fa"
	
	onMount(() => {
		body = select("body")
		setScroll($readingListVisible)
	})

	function setScroll(readingListVisible) {
		if (body) {
			if (readingListVisible == true) { body.style("overflow-y", "hidden") } 
			else { body.style("overflow-y", "auto") }
		}
	}

	function swapBarData(activeSection) {
		if (activeSection == "raunchiness") {
			barData = raunchinessData;
			barColor = "#8eacf9";
			barColorHighlight = "#4C7DFE";
		} else if (activeSection == "illustration") {
			barData = illustrationData;
			barColor = "#fde59a";
			barColorHighlight = "#F7C42D";
		} else if (activeSection == "race") {
			barData = raceData;
			barColor = "#7ce7e7";
			barColorHighlight = "#20B6B6";
		}
	}

	function calcMinDim(w, h) {
		if (w !== undefined && h !== undefined) {
			if (Math.min(w,h) > 600) { return Math.min(w, h); } 
			else { return 600 };
		} 
	}
	
	$: activeSection, swapBarData($activeSection)
	$: readingListVisible, setScroll($readingListVisible)
	$: bookMin = calcMinDim(w, h);
</script>

<svelte:window bind:innerWidth={w} bind:innerHeight={h} bind:scrollY={scrollY} />
<ChapterMarker />
<!-- CSS Grid HTML aqui -->
<div class="css-grid">
	<div id="item-0">&nbsp;</div>
	<div id="item-1">&nbsp;</div>
	<div id="item-2">&nbsp;</div>
	<div id="item-3">&nbsp;</div>
	<div id="item-4">&nbsp;</div>
	<div id="item-5">&nbsp;</div>
	<div id="item-6">&nbsp;</div>
</div>
<IntroScrolly bookMin={bookMin} w={w} h={h} scrollY={scrollY}/>
<Lookback style="z-index:9999" bookMin={bookMin}/>

<div class="sections">
	<Chapter id={"raunchiness"} data={raunchinessData} copyBlock={copy.raunchinessText} copyScroll={copy.raunchinessScroll} scrollY={scrollY} xShiftSection={$xShiftRaunch} />
	<Chapter id={"illustration"} data={illustrationData} copyBlock={copy.illustrationText} copyScroll={copy.illustrationScroll} scrollY={scrollY} xShiftSection={$xShiftIllo} />
	<Chapter id={"race"} data={raceData} copyBlock={copy.raceText} copyScroll={copy.raceScroll} scrollY={scrollY} xShiftSection={$xShiftRace} />
</div>

<Footer />

<style>
@media (min-width: 600px) {
	
.css-grid {

    position: absolute; 
    left: 0; /* Alinha a esquerda do elemento com a esquerda da viewport */
    width: 100vw; /* Define a largura do elemento para a largura total da viewport */
    height: 200vh;
    z-index: -1; 

    display: grid;
    grid-template-rows: 10fr 10fr 10fr 10fr 10fr 10fr 10fr;
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
    
  }
	#item-0 {
background-image: url('$images/card01.png');
 background-size: contain;
 background-repeat: no-repeat; 
 transform: rotate(25deg) translateY(10rem) translateX(-10rem); 
 grid-row-start: 1;
 grid-column-start: 1;
 grid-row-end: 4;
 grid-column-end: 5; 
 scale: 0.5;
 
}
#item-1 {

background-image: url('$images/card02.png');
 background-size: contain;
 background-repeat: no-repeat; 
 transform: rotate(-15deg) translateY(-10rem) translateX(-5rem);

 grid-row-start: 1;
 grid-column-start: 5;

 grid-row-end: 3;
 grid-column-end: 7;
 
 scale: 0.6;
}
#item-2 {

background-image: url('$images/card03.png');
 background-size: contain;
 background-repeat: no-repeat; 
 transform: rotate(-25deg) translateY(-5rem) translateX(-5rem);
 grid-row-start: 1;
 grid-column-start: 9;

 grid-row-end: 3;
 grid-column-end: 11;

 scale: 0.8;
 
}
#item-3 {

background-image: url('$images/card04.png');
 background-size: contain;
 background-repeat: no-repeat; 
 transform: rotate(-10deg) translateY(-10rem) translateX(-20rem);
 grid-row-start: 4;
 grid-column-start: 3;

 grid-row-end: 6;
 grid-column-end: 5;
 
 scale: 0.8;   
 
}
#item-4 {

background-image: url('$images/card05.png');
 background-size: contain;
 background-repeat: no-repeat; 
 transform: rotate(15deg) translateY(-10rem) translateX(20rem);
 grid-row-start: 4;
 grid-column-start: 7;

 grid-row-end: 6;
 grid-column-end: 9;
 scale: 0.9;
 
}
#item-5 {

background-image: url('$images/card06.png');
 background-size: contain;
 background-repeat: no-repeat; 
 transform: rotate(14deg) translateY(30rem) translateX(35rem); 
 grid-row-start: 1;
 grid-column-start: 1;
 grid-row-end: 4;
 grid-column-end: 5; 
 scale: 0.4;
}
#item-6 {

 background-image: url('$images/card07.png');
 background-size: contain;
 background-repeat: no-repeat; 
 transform: rotate(-20deg) translateY(55rem) translateX(-5rem) ;
 grid-row-start: 1;
 grid-column-start: 6;

 grid-row-end: 3;
 grid-column-end: 8;
 scale: 0.4;
 
}}

@media (max-width: 640px) {
	
	.css-grid {
	
			position: absolute; 
			left: 0; /* Alinha a esquerda do elemento com a esquerda da viewport */
			width: 100vw; /* Define a largura do elemento para a largura total da viewport */
			height: 200vh;
			z-index: -1; 
	
			display: grid;
			grid-template-rows: 10fr 10fr 10fr 10fr 10fr 10fr 10fr;
			grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
			
		}
		#item-0 {
	background-image: url('$images/card01.png');
	 background-size: contain;
	 background-repeat: no-repeat; 
	 transform: rotate(25deg) translateY(10rem) translateX(-11rem); 
	 grid-row-start: 1;
	 grid-column-start: 1;
	 grid-row-end: 4;
	 grid-column-end: 5; 
	 scale: 0.5;
	 
	}
	#item-1 {
	
	background-image: url('$images/card02.png');
	 background-size: contain;
	 background-repeat: no-repeat; 
	 transform: rotate(-15deg) translateY(2rem) translateX(-4rem);
	
	 grid-row-start: 1;
	 grid-column-start: 5;
	
	 grid-row-end: 3;
	 grid-column-end: 7;
	 
	 scale: 1.3;
	}
	#item-2 {
	
	background-image: url('$images/card03.png');
	 background-size: contain;
	 background-repeat: no-repeat; 
	 transform: rotate(5deg) translateY(3rem) translateX(-8.5rem);
	 grid-row-start: 1;
	 grid-column-start: 9;
	
	 grid-row-end: 3;
	 grid-column-end: 11;
	
	 /* scale: 1.1; */
	 
	}
	 #item-3 {
	
	background-image: url('$images/card04.png');
	 background-size: contain;
	 background-repeat: no-repeat; 
	 transform: rotate(20deg) translateY(8rem) translateX(5rem);
	 /* grid-row-start: 1;
	 grid-column-start: 9;
	
	 grid-row-end: 4;
	 grid-column-end: 11; */
	 
	 scale: 1.8;   
	 
	}

	#item-4 {
	
	background-image: url('$images/card05.png');
	 background-size: contain;
	 background-repeat: no-repeat; 
	 transform:  rotate(-20deg) translateY(35rem) translateX(-16rem);
	 grid-row-start: 1;
	 grid-column-start: 1;
	
	 grid-row-end: 4;
	 grid-column-end: 5;
	 scale: 0.6;
	 
	}
 #item-5 {
	
	background-image: url('$images/card06.png');
	background-size: contain;
	 background-repeat: no-repeat; 
	 transform:  rotate(2deg) translateY(58rem) translateX(20rem);
	 grid-row-start: 1;
	 grid-column-start: 1;
	
	 grid-row-end: 4;
	 grid-column-end: 5;
	 scale: 0.5;
	}
	
	#item-6 {
	
	background-image: url('$images/card07.png');
	background-size: contain;
	 background-repeat: no-repeat; 
	 transform:  rotate(18deg) translateY(32rem) translateX(49rem);
	 grid-row-start: 1;
	 grid-column-start: 1;
	
	 grid-row-end: 4;
	 grid-column-end: 5;
	 scale: 0.5;
	 
	}
}
</style>
