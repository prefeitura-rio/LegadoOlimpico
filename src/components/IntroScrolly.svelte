<script>
    import { onMount } from "svelte";
	import Scrolly from "$components/helpers/Scrolly.svelte";
    import IntroBook from "$components/IntroBook.svelte";
    import inView from "$actions/inView.js";
    import { activeSection } from "$stores/misc.js";
	import { Info } from "lucide-svelte";

    export let bookMin;
    export let w;
    export let h;
    export let scrollY;

    const steps = [0];

	let value;
    let loading = true;
    
    onMount(() => {
		loading = false;
	})

    function setSection(id) { activeSection.set(id); }

    $: isVisible = scrollY == undefined || scrollY < 5 ? true : false; 
</script>

<section id="intro"
    use:inView
    on:enter={() => setSection("intro")}>
	<div class="sticky">
        <IntroBook/>
    </div>
</section>

<style>
 

	.sticky {
		position: sticky;
		transition: all 1s;
        z-index: 1;
        overflow-x: hidden;
        padding: 10rem 0 0 0;
        display: flex;
        justify-content: center;
	}
	
   
    @keyframes bounceUp {
        0%       { bottom:2px; }
        25%, 75% { bottom:4px; }
        50%      { bottom:6px; }
        100%     { bottom:0; }
    }
    @keyframes rotation {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }
    @media (max-width: 640px) {
        .sticky {
		position: sticky;
		transition: all 1s;
        z-index: 1;
        overflow-x: hidden;
        padding: 2 0 0 0;
        display: flex;
        justify-content: center;
	}
    }
</style>
