<script>
  import img1 from "$images/img1.png";
  import logo_preto_horizontal from "$images/logo_preto_horizontal.png";

  let scrollPosition = 0;

  // atualize scrollPosition conforme o usuário faz scroll
  // você pode precisar ajustar isso para o seu caso de uso
  if (typeof window !== 'undefined') {
    window.addEventListener('scroll', () => {
      scrollPosition = window.scrollY;
    });
  }
</script>

<div class="relative h-screen overflow-y-scroll">
  <img id="img1" src={img1} alt="img1" class="absolute object-cover left-0 w-[100%]  opacity-0" style="opacity: {scrollPosition > 500 ? 1 : 0}" />
  <img id="logo_preto_horizontal" src={logo_preto_horizontal} alt="img2" class="absolute object-cover left-0 w-[100%] opacity-0" style="opacity: {scrollPosition > 1800 ? 1 : 0}" />
</div>