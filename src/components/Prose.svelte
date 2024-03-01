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
    import ibc from "$images/ibc.png";
</script>

<div class="prose">
    {#if copy && Array.isArray(copy)}
        {#each copy as text, i}
        {#if text.value != "foto1" &&  text.value != "foto1.1" &&  text.value != "foto1.2" && text.value != "foto2" && text.value != "foto3" && text.value != "foto4" }
            <p>{@html text.value}</p>
            {:else if text.value == "foto1"}
            <img style="padding-top: 5rem;" src={est_aqua1} alt="Foto" />
            <p class="image-caption">Estádio Aquático Olímpico. (Foto: Renato Sette Camara/Prefeitura do Rio) </p>
            {:else if text.value == "foto1.1"}
            <img style="padding-top: 5rem;" src={est_aqua2} alt="Foto" />
            <p class="image-caption">Projeto para construção do Parque Oeste (Foto: Divulgação/Prefeitura do Rio)</p>
            {:else if text.value == "foto1.2"}
            <img style="padding-top: 5rem;" src={est_aqua3} alt="Foto" />
            <p class="image-caption">Projeto para construção do Parque Oeste (Foto: Divulgação/Prefeitura do Rio)</p>
            {:else if text.value == "foto3"}
            <img style="padding-top: 5rem;" src={tg} alt="Foto" />
            <p class="image-caption">Terminal Gentileza (Foto: Marcelo Piu/Prefeitura do Rio)</p>
            {:else if text.value == "foto4"}
            <img style="padding-top: 5rem;" src={ibc} alt="Foto" />
            <p class="image-caption">Fachada do IBC (Foto: Ricardo Cassiano/Prefeitura do Rio)</p>
            {:else if text.value == "foto2"}
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
        gap:1rem
    }

    .image-container img {
        max-width: 8rem;
    }

    @media (max-width: 640px) {
        .image-container img {
            max-width: 5rem;
           
        }
        .image-container {
            justify-content: center;
            gap:0.5rem
        }
    }

    .prose {
        display: flex;
        justify-content: center;
        flex-direction: column;
        max-width: 42rem;
        margin: 0 auto;
        line-height: 2;
        padding: 0 1rem;
        font-weight: 500;
        font-size: var(--16px);
    }
    p {
        font-family: var(--serif);
        font-weight: 500;
    }

    @media (max-width: 640px) {
        .prose {
            max-width: 24rem;
            margin-left:2rem;
        }
    }

    .image-caption {
        font-size: 1rem;
    color: #333;
    line-height: 1.5rem;
    font-style: italic;
    margin-top: .2rem;
}

</style>