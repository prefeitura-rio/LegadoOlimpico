<script>
    import WallScrolly from "$components/WallScrolly.svelte";
    import ChapterText from "$components/ChapterText.svelte";
    import Bookmark from "$components/Bookmark.svelte";
    import inView from "$actions/inView.js";
    import { activeSection } from "$stores/misc.js";
    import { fly } from 'svelte/transition';
	import YardsaleScrolly from "./Yardsale.scrolly.svelte";

    import f01_esquerda from "$images/esquerda/f01d.jpg";
    import f02_esquerda from "$images/esquerda/f02b.jpg";
    import f03_esquerda from "$images/esquerda/f03.jpg";
    import f04_esquerda from "$images/esquerda/f04.jpg";
    import f05_esquerda from "$images/esquerda/f05.jpg";

    import f01_direita from "$images/direita/f01b.jpg";
    import f02_direita from "$images/direita/f02.jpg";
    import f03_direita from "$images/direita/f03.jpg";
    import f04_direita from "$images/direita/f04.jpg";
    import f05_direita from "$images/direita/f05.jpg";
  
    import { fade } from 'svelte/transition';
    
    let currentImageEsquerda = f01_esquerda;
    let currentImageDireita = f01_direita;

	let scrollDir;
	let lastY;
    let headlingFly = false;

    function getLegenda() {
    if (currentImageEsquerda === f01_esquerda) {
      return 'legenda 1';
    } else if (currentImageEsquerda === f05_esquerda) {
      return 'legenda 2';
    } else if (currentImageEsquerda === f04_esquerda) {
      return 'legenda 3';
    } else if (currentImageEsquerda === f03_esquerda) {
      return 'legenda 4';
    } else if (currentImageEsquerda === f02_esquerda) {
      return 'legenda 5';
    }

    // Caso nenhuma condição seja correspondida, retorne uma legenda padrão
    return 'legenda padrão';

  }

    let scrolly1 = [
        "A Arena do Futuro recebeu as competições de Handebol das Olimpíadas e de Goalball nas Paralimpíadas de 2016",
        "",
        "",
        "E ela não recebeu este nome à toa: o seu nome tem tudo a ver com aquilo em que ela estava destinada a se transformar. ",
        "",
        "",
        "Em março de 2022, iniciou-se a desmontagem da Arena para ser transformada em quatro escolas na Zona Oeste.",
        "",
        "",
        "Da Arena do Futuro foram aproveitados materiais como o breeze (fachada das arenas), divisórias e louças.",
        "",
        "",
        "Dois, dos quatro ginásios previstos já foram inaugurados: o GET (Ginásio Experimental Tecnológico) José Mauro de Vasconcelos, em Bangu, e o GET Emiliano Galdino, em Santa Cruz.",
        "",
        "",
        "As outras duas escolas, que estão sendo construídas no bairro de Campo Grande e Rio das Pedras, tem previsão de inauguração para o primeiro semestre deste ano.",
        "",
        "",
        "As unidades de ensino possuem o modelo de escola pública mais inovador do país, que segue a abordagem STEAM (Ciência, Tecnologia, Engenharia, Artes e Matemática).",
        "",
        "",
        "Esse modelo investe na qualificação da educação integral e desenvolve uma aprendizagem baseada em projetos, atividades mão na massa e recursos que promovam a cultura digital.",
        "",
        ""
  ]

    export let id;
    export let copyBlock;
    export let scrollY;

    function setSectionEnter(id) { 
        headlingFly = true;
        activeSection.set(id); 
    }
    function setSectionExit(id) { 
        let nextSection;
        if (scrollDir == "down") {
            if (id == "raunchiness") { nextSection = "illustration"; } 
            else if (id == "illustration") { nextSection = "race"; }
            else if (id == "race") { nextSection = "methods"; }
            activeSection.set(nextSection)
        } else if (scrollDir == "up") {
            if (id == "raunchiness") { nextSection = "intro"; } 
            else if (id == "illustration") { nextSection = "raunchiness"; }
            else if (id == "race") { nextSection = "illustration"; }
            activeSection.set(nextSection)
        }
    }

    function checkScrollY(scrollY) {
        if (scrollY) {
            scrollDir = scrollY > lastY ? "down" : "up"
            lastY = scrollY;
        }
    }

    
    $: scrollY, checkScrollY(scrollY);
    let legenda;

$: {
    if (currentImageEsquerda === f01_esquerda) {
      legenda = 'Clique nos botões abaixo.';
    } else if (currentImageEsquerda === f05_esquerda) {
      legenda = 'Arquibancadas';
    } else if (currentImageEsquerda === f04_esquerda) {
      legenda = 'Fachada';
    } else if (currentImageEsquerda === f03_esquerda) {
      legenda = 'Drywall';
    } else if (currentImageEsquerda === f02_esquerda) {
      legenda = 'Louças';
    } else {
      legenda = 'legenda padrão';
    }
}
</script>

<section id={id}
    use:inView={{ top: 0 }}
    on:enter={() => setSectionEnter(id)}
    on:exit={() => setSectionExit(id)}>
    {#if headlingFly }
        <!-- <h2 in:fly={{ y: 200, duration: 2000 }}>{resetTitles(id)}</h2> -->
        {#if id == "raunchiness"}
            <YardsaleScrolly words={scrolly1} container="scrolly1"  />
        {/if}
        {#if id == "illustration"}
        <div class="legenda"> {legenda}</div>
        <div class="container">
           
            <div class="image-container">
                <img class="img2_left" src={currentImageEsquerda} alt="img2_left" in:fade={{ delay: 0 }} out:fade />
               <!--reseta / images iniciais-->
                <button class="image-button" style="top: 68%; left: 63%;" on:click={() => (currentImageEsquerda = f01_esquerda) && (currentImageDireita = f01_direita)}>+</button>
                <!--arquibancada-->
                <button class="image-button" style="top: 53%; left: 40%;" on:click={() => (currentImageEsquerda = f05_esquerda) && (currentImageDireita = f05_direita)}>+</button>
                <!--fachada-->
                <button class="image-button" style="top: 65%; left: 10%;" on:click={() => (currentImageEsquerda = f04_esquerda) && (currentImageDireita = f04_direita)}>+</button>
                <!--drywall-->
                <button class="image-button" style="top: 77%; left: 30%;" on:click={() => (currentImageEsquerda = f03_esquerda) && (currentImageDireita = f03_direita)}>+</button>
               <!--louças-->
                <button class="image-button" style="top: 53%; left: 90%;" on:click={() => (currentImageEsquerda = f02_esquerda) && (currentImageDireita = f02_direita)}>+</button>
            </div>
            <img src={currentImageDireita} alt="currentImage" in:fade={{ delay: 0 }} out:fade />
        </div>
        {/if}
    {/if}
    <ChapterText copy={copyBlock}/>
</section>

<style>
.legenda{
    display: flex;
    justify-content: center;
    flex-direction: column;
    max-width: 38rem;
    margin: 0 auto;
    padding: 1rem; 
    border: 1px solid #333; 
    text-align: center;
    border-radius: 50px;
    background-color: #f5f5f5; 
    color: #333; 
    box-shadow: 0 2px 4px rgba(0, 0, 0.1, 0.1);
    margin-bottom: 20px !important;
}
@media (max-width: 640px) {
    .legenda {
        max-width: 24rem;
    }
}
.container {
  margin: 0 auto;
  display: flex;
  justify-content: flex-start;
  width: 100%;
}

.container .image-container, .container img {
  width: 50%;
  flex: 1;
}

.image-container {
  position: relative;
}

.image-container img {
  width: 100%;
}

/* Adicione esta consulta de mídia para alterar a largura em dispositivos móveis */
@media screen and (max-width: 640px) {
  .container .image-container, .container img {
    width: 100%;
  }
}

.image-button {
  position: absolute;
  width: 30px; 
  height: 30px; 
  border-radius: 50%;
  background-color: black;
  text-align: center;
  padding: 0;
  border: none;
  color: white;
  font-size: 20px; 
}

@media (max-width: 640px) {
  .container {
    flex-direction: column;
  }

  .container img {
    width: 100%;
  }
}
    section {
        padding: 3rem 0;
    }
    #raunchiness {
        /* background-image: linear-gradient(var(--romance-bg-pink) 0%, var(--romance-bg-blue) 10%); */
    }
    #illustration {
        /* background-image: linear-gradient(var(--romance-bg-blue) 0%, var(--romance-bg-yellow) 10%); */
    }
    #race {
        /* background-image: linear-gradient(var(--romance-bg-yellow) 0%, var(--romance-bg-teal) 10%); */
    }
    :global(section a) {
		color: var(--color-gray-800);
		background-repeat: no-repeat;
        transition: background-position .08s ease-out;
        background-position: 0 1.125rem;
		border-bottom: none;
		pointer-events: auto;
	}
    :global(#raunchiness a) {
		/* background-image: linear-gradient(180deg,transparent 0,var(--romance-blue-light) 0); */
	}
	:global(#illustration a) {
		/* background-image: linear-gradient(180deg,transparent 0,var(--romance-yellow-light) 0); */
	}
	:global(#race a) {
		/* background-image: linear-gradient(180deg,transparent 0,var(--romance-teal-light) 0); */
	}
    :global(#intro a) {
		/* background-image: linear-gradient(180deg,transparent 0,var(--romance-pink-light) 0); */
	}
    :global(#methods a) {
        /* background-image: linear-gradient(180deg,transparent 0,var(--romance-pink-light) 0); */
        background-position: 0 1.05rem;
    }
    :global(section a:hover) {
		background-position: 0 0;
	}
    h2 {
        display: flex;
        justify-content: center;
        flex-direction: column;
        width: 100%;
        margin: 0 auto 4rem auto;
        text-align: center;
        text-transform: capitalize;
        font-family: var(--serif-display);
        font-size: var(--44px);
        padding: 3rem 0 0 0;
        z-index: 100;
        position: relative;
        overflow: hidden;
        min-height: 15rem;
    }
    h2:after {
        position: absolute;
        font-family: var(--sans-display);
        font-weight: 900;
        font-size: 200px;
        text-align: center;
        left: 50%;
        transform: translate(-50%, -10%);
        text-transform: uppercase;
        pointer-events: none;
        z-index: -1;
        letter-spacing: -0.5rem; 
    }
    /* :global(#raunchiness h2:after) {
        content: "Raunchiness";
        background: linear-gradient(to bottom, rgba(142, 172, 249, 0) 15%, rgba(142, 172, 249, 1));
        -webkit-text-fill-color: transparent;
        -webkit-background-clip: text;
        opacity: 0.25;
    }
    :global(#illustration h2:after) {
        content: "Illustration";
        background: linear-gradient(to bottom, rgba(253, 229, 154, 0) 15%, rgba(253, 229, 154, 1));
        -webkit-text-fill-color: transparent;
        -webkit-background-clip: text;
        opacity: 0.5;
    }
    :global(#race h2:after) {
        content: "Diversity";
        background: linear-gradient(to bottom, rgba(124, 231, 231, 0) 15%, rgba(124, 231, 231, 1));
        -webkit-text-fill-color: transparent;
        -webkit-background-clip: text;
        opacity: 0.35;
    } */
    @media only screen and (min-width: 600px) {
        section {
            padding: 3rem 0;
        }
        h2 {
            font-size: var(--64px);
        }
        h2:after {
            font-size: 300px;
        }
	}
</style>