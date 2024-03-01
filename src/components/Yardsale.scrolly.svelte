<script>
	import { onMount } from "svelte";
	import Scrolly from "$components/helpers/Scrolly.svelte";
	import { fade } from "svelte/transition";
	export let words; // words from google doc

	export let container; // container name, ie "scrolly3"
	let currentStageNumber = 0; // stage number
	let currentStage; // full stage name, ie "scrolly3-1"

	let value = 0; // current step, binded to scroll
	let containerHeight;
	let stepHeight;
	let stepWidth;
	let panelHeight = stepWidth * 0.8;
	let bgColor = "#000";
	let bgOpacity = 1;
	let r = 0;
	let currentText;
	let currentLocation = 0;
	let progress;
	let loaded = 0;

	// Keyframes for each stage
	const stageLookup = {
		"scrolly1-0": [
			{"image":"f01", "xmetric":"left", "x":0, "ymetric": "top", "y":0, "width": 105, "opacity": 1}
			],
		"scrolly1-1": [
			{"image":"f02", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-2": [
			{"image":"f03", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-3": [
			{"image":"f04", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-4": [
			{"image":"f05", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-5": [
			{"image":"f06", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-6": [
			{"image":"f07", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-7": [
			{"image":"f08", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-8": [
			{"image":"f09", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-9": [
			{"image":"f10", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-10": [
			{"image":"f11", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-11": [
			{"image":"f12", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-12": [
			{"image":"f13", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-13": [
			{"image":"f14", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-14": [
			{"image":"f15", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-15": [
			{"image":"f16", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-16": [
			{"image":"f17", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-17": [
			{"image":"f18", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-18": [
			{"image":"f19", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-19": [
			{"image":"f20", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-20": [
			{"image":"f21", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-21": [
			{"image":"f22", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-22": [
			{"image":"f23", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-23": [
			{"image":"f24", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-24": [
			{"image":"f25", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			],
		"scrolly1-25": [
			{"image":"f26", "xmetric":"left","x":-20, "ymetric": "top", "y":-20, "width": 140, "opacity": 1},
			]
	};

	// Runs on new stage
	function newScroll(v) {
		v = v == undefined ? currentStageNumber : v;
		currentStageNumber = v;
		currentStage =
			v == undefined
				? stageLookup[container + "-0"]
				: stageLookup[container + "-" + v];

		// sets backgroudn colors for scrolly
		if (container == "scrolly1" && currentStageNumber == 0) {
			bgColor = "#000";
			bgOpacity = 0.5;
		} else if (container == "scrolly3") {
			bgColor = "#c8becf";
			bgOpacity = 0.3;
		} else {
			bgColor = "#7c6a85";
			bgOpacity = 0.5;
		}
	}

	let currentProgress = 0;
	function getProgress() {
		try {
			currentProgress =
				(currentStageNumber + progress[currentStageNumber] / 2) / words.length;
		} catch {
			currentProgress = 0;
		}
		if (currentProgress > 1) {
			currentProgress = 1;
		}
	}

	let marginTop = 0;
	setInterval(function () {
		if (stepWidth != undefined) {
			loaded = 1;
		}
	}, 100);
	$: {
		newScroll(value);
		currentStage = currentStage;
		stepWidth = stepWidth;
		stepHeight = stepHeight;
		containerHeight = containerHeight;
		panelHeight = stepWidth;
		currentText = words[currentStageNumber];
		progress = progress;
		getProgress();
	}
</script>

<svelte:window bind:innerHeight={containerHeight} />
<div class="interactive_container">
	<section class="scrolly" id={container}>
		<div
			class="scrollyBackground"
			bind:clientHeight={stepHeight}
			bind:clientWidth={stepWidth}
		>
			<div >
				<!-- If it's not the third scrolly, display the comic -->
				{#if container != "scrolly3"}
					{#each currentStage as { image,opacity }}
					<img
					class={image}
					src="assets/yardsale/art/{image}.jpg"
					alt="stageImage"
					style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; object-fit: cover; opacity:{opacity};"
					in:fade={{ delay: 0 }}
					out:fade
			/>
					{/each}
					
				{/if}

			</div>
		</div>

		<div class="scrollyContainer">
			<Scrolly bind:value bind:progress>
				{#each words as text, i}
					{@const active = value === i}
					{#if text != ""}
						<div class="step step{i}" class:active style="opacity: {loaded};">
							{#if container == "scrolly3" && currentStageNumber == 2 && r > 1500 && r < 4500}
								<p>Still simulating 10,000 rounds...</p>
							{:else if container == "scrolly3" && currentStageNumber == 2 && r > 4500 && r < 10000}
								<p>Seriously, just wait...</p>
							{:else if container == "scrolly3" && currentStageNumber == 2 && r == 10000}
								<p>
									Whoa, you lost all your money. Meanwhile, one person ended up
									with nearly all of the wealth!
								</p>
							{:else}
								<p>{text}</p>
							{/if}
						</div>
					{:else}
						<div class="step step{i} stepHidden" class:active>
							<p>{text}</p>
						</div>
					{/if}
				{/each}
			</Scrolly>
		</div>
	</section>
</div>

<style>
	.interactive_container {
		padding: 10px 0;
		font-family: "National 2 Web", sans-serif;
	}

	.gameContainer {
		display: block;
		position: absolute;
		top: 40px;
		width: 100%;
		color: white;
		font-size: 22px;
		line-height: 1.3em;
		font-family: "National 2 Web", sans-serif;
	}
	
	@media only screen and (max-width: 640px) {
		.gameContainer {
			top: 20px;
			font-size: 15px;
			line-height: 18px;
		}
	}
	
	.gameInfoItem {
		width: 100%;
		position: relative;
	}
	.gameInfoFullbar {
		width: 70%;
		position: absolute;
		height: 20px;
		border: 2px solid var(--category-bg-purple);
		background: var(--category-purple2);
		left: 0;
		top: 0;
		margin-top: 4px;
	}
	@media only screen and (max-width: 640px) {
		.gameInfoFullbar {
			height: 10px;
		}
	}
	.gameInfoBar {
		height: 100%;
		background: var(--category-bg-purple);
		position: absolute;
		left: 0;
		top: 0;
	}
	
	.scrolly {
		/* max-width: 1100px; */
		margin: 0px auto;
		min-height: 100vh;
	}
	.scrollyContainer {
		width: 100%;
		margin-top: -200px;
		z-index: 3;
		pointer-events: none;
	}
	.scrollyBackground {
		position: sticky;
		top: 0;
		/* width: 100%; */
		/* margin: auto auto; */
		height: 100vh;
		/* border: 3px solid #000; */
		/* max-width: 95vh; */
		z-index: -1;
		transition: opacity 500ms cubic-bezier(0.25, 0.25, 0.75, 0.75);
	}
	.scrollyImageContainer {
		width: 100%;
		height: 100%;
		position: absolute;
		left: 0;
		top: 0;
		overflow: hidden;
	}

	.fuzzy {
		animation: grain 20s steps(10) infinite;
		content: "";
		height: 500%;
		width: 500%;
		opacity: 1;
		position: absolute;
		left: -125%;
		top: -125%;
		pointer-events: none;
	}
	@keyframes grain {
		0%,
		100% {
			transform: translate(0, 0);
		}
		10% {
			transform: translate(-5%, -10%);
		}
		20% {
			transform: translate(8%, 5%);
		}
		30% {
			transform: translate(-7%, -5%);
		}
		40% {
			transform: translate(5%, 20%);
		}
		50% {
			transform: translate(-15%, -10%);
		}
		60% {
			transform: translate(0%, 0%);
		}
		70% {
			transform: translate(0%, -12%);
		}
		80% {
			transform: translate(-10%, 12%);
		}
		90% {
			transform: translate(10%, -10%);
		}
	}
	.scrolldown_hint {
		position: absolute;
		width: 0;
		height: 0;
		border-left: 20px solid transparent;
		border-right: 20px solid transparent;
		border-top: 20px solid black;
		right: 50%;
		margin-right: -10px;
		top: calc(100% + 50px);
		margin-left: -5px;
		opacity: 0.4;
		z-index: 1000;
		animation: bounce 1s ease infinite;
	}
	.scrolldown_words {
		position: absolute;
		width: 120px;
		left: 50%;
		margin-left: -60px;
		font-weight: bold;
		text-align: center;
		bottom: 22px;
		color: black;
		text-transform: uppercase;
	}
	.scrollyBackground img {
		position: absolute;
		width: 100%;
		max-width: none !important;
		transition: all 800ms cubic-bezier(0.25, 0.1, 0.25, 1);
		transition-timing-function: cubic-bezier(0.25, 0.1, 0.25, 1);
	}

	.player1-happy,
	.player2-happy,
	.player3-happy,
	.player1-sad,
	.player2-sad,
	.player3-sad {
		background: #c5b3c7;
	}
	.player1-happy.happy,
	.player2-happy.happy,
	.player3-happy.happy {
		background: #f5cd49;
	}

	.scrollyBackground .hidden {
		opacity: 0;
	}
	.step {
		display: block;
		height: 100vh;
		text-align: left;
		width: 100%;
		min-width: 200px;
		box-sizing: border-box;
		transition: opacity 500ms cubic-bezier(0.25, 0.25, 0.75, 0.75);
	}
	.step.stepHidden {
		opacity: 0;
		pointer-events: none;
	}
	.step > p {
		font-family: "";
		max-width: 580px;
		margin: 0 auto;
		background: rgba(255, 2595, 2595, 0.95);
		font-size: 1.2em;
		padding: 50px;
		box-sizing: border-box;
		color: black;
		/* text-shadow: -1px -1px 6px rgba(0, 0, 0, 0.5); */
		text-align: justify;
		border-radius: 12px;
		/* border: 1px solid black; */
	}

	@media only screen and (max-width: 640px) {
		.scrollyBackground {
			margin: 0% auto;
			min-height: none;

			float: none;
			width: 110%;
			top: 25%;
			height: 60vh;
		}
		.step > p {
			width: 90%;
		}
	}
</style>
