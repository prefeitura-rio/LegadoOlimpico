<script>
	export let copy;
	// import card01 from "$images/card01.png";
	// import card02 from "$images/card02.png";
	// import card03 from "$images/card03.png";
	// import card04 from "$images/card01.png";
	// import card05 from "$images/card02.png";
	// import card06 from "$images/card03.png";
	import est_aqua1 from "$images/est_aqua1.png";
	import est_aqua2 from "$images/est_aqua2.png";
	import est_aqua3 from "$images/est_aqua3.png";
	import tg from "$images/tg.png";
	// import ibc from "$images/ibc.png";
</script>

<div class="prose">
	{#if copy && Array.isArray(copy)}
		{#each copy as text, i}
			{#if text.value != "foto1" && text.value != "foto1.1" && text.value != "foto1.2" && text.value != "foto2" && text.value != "foto3" && text.value != "foto4" && text.value != "foto5"}
				{#if text.card && text.card == "card01"}
					<div style="display:flex; justify-content:center">
						<img
							class="card1Img"
							src="assets/yardsale/art/card01.jpg"
							alt="Foto"
						/>
						<p class="card1Texto">
							{@html text.value}
						</p>
					</div>
				{/if}
				{#if text.card && text.card == "card06"}
					<div style="display:flex; justify-content:center">
                        <p class="card2Texto">
							{@html text.value}
						</p>
						<img
							class="card2Img"
							src="assets/yardsale/art/card06.jpg"
							alt="Foto"
						/>
						
					</div>
				{/if}
				{#if text.card && text.card == "card05"}
					<div style="display:flex; justify-content:center">
                        <p class="card5Texto">
							{@html text.value}
						</p>
						<img
							class="card5Img"
							src="assets/yardsale/art/card05.jpg"
							alt="Foto"
						/>
						
					</div>
				{/if}
				{#if !text.card}
					<p>{@html text.value}</p>
				{/if}
			{:else if text.value == "foto1"}
				<!-- <img style="padding-top: 5rem;" src={est_aqua1} alt="Foto" />
				<p class="image-caption">
					Estádio Aquático Olímpico.<br /> (Foto: Renato Sette Camara/Prefeitura
					do Rio)
				</p> -->
				<iframe id="teste" allow="fullscreen" allowfullscreen height="400" src="https://streamable.com/e/3cyhpg?muted=1&nocontrols=1&autoplay=1" width="670" style="border:none;"></iframe>

				<p class="image-caption">
					Os cariocas poderão nadar na mesma piscina que o atleta Michael Phelps nadou nas Olimpíadas.
				</p> 
				<!-- {:else if text.value == "foto1.1"}
				<img style="padding-top: 5rem;" src={est_aqua2} alt="Foto" />
				<p class="image-caption">
					Projeto para construção do Parque Oeste <br />(Foto:
					Divulgação/Prefeitura do Rio)
				</p> -->
			<!-- {:else if text.value == "foto1.2"}
				<img style="padding-top: 5rem;" src={est_aqua3} alt="Foto" />
				<p class="image-caption">
					Projeto para construção do Parque Oeste<br /> (Foto: Divulgação/Prefeitura
					do Rio)
				</p> -->
			{:else if text.value == "foto3"}
			<img style="padding-top: 5rem;" src="assets/yardsale/art/ibc.jpg" alt="Foto" />
				<p class="image-caption">
					Fachada do IBC <br />(Foto: Ricardo Cassiano/Prefeitura do Rio)
				</p>
			
			{:else if text.value == "foto4"}
			<img style="padding-top: 5rem;" src={tg} alt="Foto" />
			<p class="image-caption">
				Terminal Gentileza <br />(Foto: Marcelo Piu/Prefeitura do Rio)
			</p>
			{:else if text.value == "foto2"}
				<div class="image-container">
					<iframe
						width="670"
						height="400"
						src="https://www.youtube.com/embed/d1bsrglUj6A?si=JQBsI3PdFvW1zrQ7"
						title="YouTube video player"
						frameborder="0"
						allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
						allowfullscreen
					></iframe>
				</div>
			{:else if text.value == "foto5"}
				<div class="image-container">
					<img src="assets/yardsale/art/card01.jpg" alt="Foto" />
					<img src="assets/yardsale/art/card02.jpg" alt="Foto" />
					<img src="assets/yardsale/art/card03.jpg" alt="Foto" />
					<img src="assets/yardsale/art/card04.jpg" alt="Foto" />
					<img src="assets/yardsale/art/card05.jpg" alt="Foto" />
					<img src="assets/yardsale/art/card06.jpg" alt="Foto" />
					<img src="assets/yardsale/art/card07.jpg" alt="Foto" />
				</div>
			{/if}
		{/each}
	{:else}
		<p>{@html copy.value}</p>
	{/if}
</div>

<style>

	.image-container {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		padding-bottom: 5rem;
		padding-top: 6rem;
		gap: 1rem;
		scale: 1.1;
	}

	.image-container img {
		max-width: 8rem;
	}

	@media (max-width: 640px) {
		#teste{
			width: 105vw;
			margin-left: -1.2rem;
		}
		.image-container img {
			max-width: 5rem;
		}
		.image-container {
			justify-content: center;
			gap: 0.5rem;
		}
		.image-caption {
			text-align: left;
		}
	}

	.prose {
		display: flex;
		justify-content: center;
		flex-direction: column;
		max-width: 42rem;
		margin: 0 auto;
		line-height: 2;
		/* padding: 0 1rem; */
		font-weight: 500;
		font-size: var(--16px);
		text-align: justify;
	}
	p {
		font-family: var(--serif);
		font-weight: 500;
	}

	@media (max-width: 640px) {
		.prose {
			/* max-width: 26rem; */
			/* margin-left:2.2rem; */
		}
        .card1Img{
            display: none;
        }
        .card2Img{
            display:none;
        }
        .card5Img{
            display:none;
        }
	}

    @media (min-width: 640px) {
        .card1Img {
            width:10rem;
            transform: translate(-12rem) rotate(-12deg);
        }
        .card1Texto {
            min-width:42rem !important;
            transform: translate(-5rem)
        }
        .card2Img {
            width:10rem;
            transform: translate(12rem) rotate(12deg);
        }
        .card2Texto {
            min-width:42rem !important;
            transform: translate(5rem)
        }
        .card5Img {
            width:10rem;
            transform: translate(12rem) rotate(12deg);
        }
        .card5Texto {
            min-width:42rem !important;
            transform: translate(5rem)
        }
    }
    @media (max-height: 500px) and (orientation: landscape) {
        .card1Img{
            display: none;
        }
        .card1Texto {
            /* min-width:42rem !important; */
            transform: translate(-0rem)
        }
        .card2Img{
            display:none;
        }
        .card2Texto {
            /* min-width:42rem !important; */
            transform: translate(-0rem)
        }
        .card5Img{
            display:none;
        }
        .card5Texto {
            /* min-width:42rem !important; */
            transform: translate(-0rem)
        }
    }

	.image-caption {
		font-size: 1rem;
		color: #333;
		line-height: 1.5rem;
		font-style: italic;
		margin-top: 0.2rem;
	}
</style>
