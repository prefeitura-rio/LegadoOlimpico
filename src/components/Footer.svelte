<!-- src/components/Footer.svelte -->

<script>
  import logo from "$svg/logo.svg"; 
	// import { activeBar } from "$stores/misc.js";
</script>


 <footer class="footer">
	<h3 id="autores">Autores</h3>
	<h6>Caio Jacintho</h6>
	<h6>Judite Cypreste</h6>
	<h6>Pedro Meneghel</h6>
	<h6>Lucas Tavares</h6>
  
	<br>
	<br>
	<h3 id="agradecimentos">Agradecimentos</h3>
	<h6>Cláudia Escarlate</h6>
	<h6>João Carabetta</h6>
	<h6>Joice Nascimento</h6>
	<h6>Michel Castellar</h6>
	<h6>Pedro Simões</h6>
	<h6>Rafael Lisboa</h6>
	<h6>Teresa Fayal</h6>

	<br>
	<br>
	<h3 id="prefeito">Prefeito</h3>
	<h6>Eduardo Paes</h6>
	<div class="footer_logo">
		<img style="width: 200px;" src="assets/yardsale/art/logo_preto_horizontal.png" alt="Foto" />
	</div>
	<br>
	<br>
 </footer>
 
 <style>
	#autores, #agradecimentos, #prefeito{
		font-size: 25px;
	}
	.footer_logo{
		padding:150px;
	}
	.footer {
	margin-top: 20vh;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	padding: 20px;

}
	.footer h3,
	.footer h6 {
		margin: 0 20px 10px;
		font-size: 15px;
	}
	
	.footer h3{
		font-weight: bold
	}
	.logo{
		margin: 0 20px 10px;
	}
 
	.footer img {
		width: 100px;
		height: auto;
	}
 </style>
 