<script>
	import { getContext } from "svelte";
	import { selectAll, style } from "d3-selection";

	export let bookMin;
	export let w;
	export let h;
	export let scrollY;

	const copy = getContext("copy");

</script>

<div class="container">
  <div class="title">
    <h2 id="sem_elefantes">Sem elefantes brancos</h2>
		<!-- <h1 style="font-size:90px;font-weight:bold"></h1> -->
    <h6 style="font-size:20px;">Explorando a Arquitetura Nômade nas Olimpíadas do Rio 2016</h6>
  </div>

  <!-- <div class="css-grid">
    <div id="item-0">&nbsp;</div>
    <div id="item-1">&nbsp;</div>
    <div id="item-2">&nbsp;</div>
    <div id="item-3">&nbsp;</div>
    <div id="item-4">&nbsp;</div>
    <div id="item-5">&nbsp;</div>
    <div id="item-6">&nbsp;</div>
  </div> -->
</div>

<style>
.container {
  position: relative;
	height: 65vh;
	overflow: hidden;
}

.title {
  position: absolute;
  z-index: 2 !important;
  display: flex;
  justify-content: center;
  align-items: center;
	flex-direction: column;
  height: 50vh;
  width: 100%;
  text-align: center;
}
#sem_elefantes {
	font-size: 5rem;
}
@media (max-width: 640px) {
	
	#sem_elefantes {
		padding-top: 8rem;
		padding-bottom: 1.5rem;
	font-size: 3rem;
	line-height: 2.8rem;
}
}

@media only screen and (max-height: 500px) and (orientation: landscape) {
	.title {
	height: 55vh;
	}
}


/* .css-grid {
	position: inherit;
	z-index: 1 !important;
  display: grid;
	grid-template-rows: 10fr 10fr 10fr 10fr 10fr 10fr 10fr ;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  gap: 0px;
  height: 60rem;
} */
  
/* #item-0 {

	background-image: url('$images/card01.png');
   background-size: cover;
   background-repeat: no-repeat; 
   transform: rotate(25deg) ; 
   grid-row-start: 1;
   grid-column-start: 1;
	 grid-row-end: 3;
	 grid-column-end: 3; 
   scale: 1.2;
   
}
#item-1 {

	background-image: url('$images/card02.png');
   background-size: cover;
   background-repeat: no-repeat; 
   transform: rotate(-15deg) translateY(-80px) translateX(-80px);

	 grid-row-start: 1;
   grid-column-start: 5;

   grid-row-end: 3;
   grid-column-end: 7;
   
   scale: 0.8;
}
#item-2 {

	background-image: url('$images/card03.png');
   background-size: cover;
   background-repeat: no-repeat; 
   transform: rotate(10deg) translateY(-200px) translateX(-100px);
   grid-row-start: 1;
   grid-column-start: 9;

   grid-row-end: 3;
   grid-column-end: 11;
   
}
#item-3 {

  background-image: url('$images/card04.png');
   background-size: cover;
   background-repeat: no-repeat; 
   transform: rotate(-10deg) translateY(40px) translateX(-80px);
   grid-row-start: 4;
   grid-column-start: 3;

   grid-row-end: 6;
   grid-column-end: 5;
   
   scale: 0.8;   
   
}
#item-4 {

	background-image: url('$images/card05.png');
   background-size: cover;
   background-repeat: no-repeat; 
   transform: rotate(15deg) translateY(-140px) translateX(120px);
   grid-row-start: 4;
   grid-column-start: 7;

   grid-row-end: 6;
   grid-column-end: 9;
   scale: 1.2;
   
}
#item-5 {

	background-image: url('$images/card06.png');
   background-size: cover;
   background-repeat: no-repeat; 
   transform: rotate(15deg);
   grid-row-start: 7;
   grid-column-start: 1;

   grid-row-end: 9;
   grid-column-end: 3;
   scale: 0.8;
}
#item-6 {

  background-image: url('$images/card07.png');
   background-size: cover;
   background-repeat: no-repeat; 
   transform: rotate(-15deg);
   grid-row-start: 7;
   grid-column-start: 5;

   grid-row-end: 9;
   grid-column-end: 7;
   
   scale: 0.8;
   
} */
/* #item-7 {

   background-color: #9A5DDD; 
   grid-row-start: 7;
   grid-column-start: 9;

   grid-row-end: 9;
   grid-column-end: 11;
   
} */

	#intro-book {
		position: sticky;
		top: 0rem;
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		margin: 0 0 0 0;
		padding: 1rem 0 2rem 0;
	}
	.credit {
		font-size: var(--12px);
		color: var(--color-gray-800);
		font-family: var(--sans-display);
		text-align: center;
		margin: -0.5rem 1rem 0 1rem;
		z-index: 1000;
	}
	.credit a {
		color: var(--color-gray-800);
		background-position: 0 0.9rem;
	}
	.credit a:hover {
		background-position: 0 0;
	}
	#book {
		margin: 0 auto;
		position: relative;
		perspective: 2000px;
		transform: translate3d(0, 0, 0);
		padding: 1rem;
		max-width: 640px;
		max-height: 740px;
		min-width: 200px;
		min-height: 400px;
		transition: all 0.5s;
		aspect-ratio: 1 / 1.475;
		height: 80vmin;
	}
	/* #book:hover .main:hover {
		transform:rotate3d(0,1,0,-30deg);
	} */
	.main {
		width: 100%;
		height: 100%;
		color: var(--color-off-black);
		position: relative;
		padding: 32% 0 0 0;
		transform-style: preserve-3d;
		transition-duration: 0.5s;
		aspect-ratio: 1/1.475;
	}

	/* = Book Font
-------------------------------------------------------------- */
	.book-front {
		width: 100%;
		height: calc(100% - 1rem);
		position: absolute;
		top: 0;
		bottom: 0;
		font-size: 15px;
		text-align: center;
		box-shadow: inset 3px 0 10px rgba(0, 0, 0, 0.1); /* 给书本添加光照阴影 */
		z-index: 10;
		transform-style: preserve-3d;
		transform-origin: 0% 50%;
		transition-duration: 0.5s;
		transform: translate3d(0, 0, 25px);
	}
	.book-cover {
		width: 100%;
		height: 100%;
		overflow: hidden;
		position: absolute;
		top: 0;
		bottom: 0;
		background-color: var(--romance-blue);
		background-size: cover;
		background-repeat: no-repeat;
		transform-style: preserve-3d;
		backface-visibility: hidden;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: space-between;
		box-shadow:
			-15px 15px 20px -3px rgba(0, 0, 0, 0.125),
			inset -1px 1px 2px rgba(255, 255, 255, 0.5);
	}
	.img-wrapper {
		position: absolute;
		width: 100%;
		height: 100%;
	}
	.img-wrapper img {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}
	.gradient-wrapper {
		position: absolute;
		width: 100%;
		height: 100%;
		background-image: linear-gradient(
			to right,
			rgba(60, 13, 20, 0.25) 1px,
			rgba(255, 255, 255, 0.5) 3px,
			rgba(255, 255, 255, 0.25) 7px,
			rgba(255, 255, 255, 0.25) 10px,
			transparent 12px,
			transparent 16px,
			rgba(255, 255, 255, 0.25) 17px,
			transparent 22px
		);
		/* url("/assets/images/Alice_cover_notype.jpg"); */
	}
	.title-wrapper {
		position: absolute;
		container: title / inline-size;
	}
	.book-cover h1 {
		font-family: var(--sans-display);
		font-weight: 900;
		font-style: normal;
		text-transform: uppercase;
		color: #f8dc3f;
		line-height: 2;
		margin: 0 auto 0 auto;
		padding: 0 0 5rem 0;
		text-align: center;
		width: 100%;
		text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.25);
		max-height: 60%;
		white-space: nowrap;
		font-size: 36px;
		/* transition: all 0.5s; */
	}
	
	.book-cover .byline {
		font-family: var(--serif-display);
		position: absolute;
		bottom: 0.5rem;
		/* font-weight: 900; */
		font-style: normal;
		text-align: center;
		width: 100%;
		font-size: var(--24px);
		color: #f8dc3f;
		margin: 0;
	}
	.byline a {
		color: #f8dc3f;
		background-image: none !important;
	}
	.byline a:hover {
		color: var(--romance-yellow-light);
	}
	.book-cover-back {
		width: 100%;
		height: 100%;
		position: absolute;
		top: 0;
		bottom: 0;
		background: #4c7dfe;
		transform-style: preserve-3d;
		backface-visibility: hidden;
		transform: rotate3d(0, 1, 0, -180deg);
		box-shadow: -15px 15px 20px -3px rgba(0, 0, 0, 0.125);
	}
	.book-cover-back-indent {
		width: calc(100% - 1rem);
		height: calc(100% - 2rem);
		background: white;
		margin-top: 1rem;
		margin-left: 1rem;
		box-shadow: inset -3px 0 10px rgba(0, 0, 0, 0.1);
		padding: 2rem 1rem;
	}

	.book-cover-back-indent p {
		font-family: var(--serif);
		font-weight: 500;
		font-size: 16px;
		line-height: 1.65;
		margin: 0 0 1rem 0;
		text-align: left;
		padding: 0 0 1rem 0;
	}

	:global(.initial-cap) {
		float: left;
		font-family: var(--serif-display);
		font-weight: 600;
		font-size: 50px;
		line-height: 0.8;
		margin: 0.25rem 0 0 0;
		padding: 0 0.25rem 0 0;
		position: relative;
		z-index: 1000;
	}

	/* = Book Page
-------------------------------------------------------------- */
	.book-page {
		width: calc(100% - 1rem);
		height: calc(100% - 3rem);
		line-height: 20px;
		position: absolute;
		top: 1rem;
		z-index: 9;
		box-shadow: inset 3px 0 10px rgba(0, 0, 0, 0.1);
		transform-style: preserve-3d;
		transition-duration: 0.5s;
		transform-style: preserve-3d;
		transform: translate3d(0, 0, 24px);
	}
	.page {
		height: 100%;
		padding: 2rem 2rem;
		overflow: hidden;
	}
	.book-page p {
		font-size: 16px;
		line-height: 1.65;
		margin: 0 0 1rem 0;
		padding: 0 0 1rem 0;
		font-family: var(--serif);
	}

	/* = Book Back
-------------------------------------------------------------- */
	.book-back {
		width: 100%;
		height: calc(100% - 1rem);
		background: #4c7dfe;
		position: absolute;
		top: 0;
		bottom: 0;
		transform: rotate3d(0, 1, 0, -180deg) translate3d(0, 0, 25px);
		z-index: 8;
		box-shadow: -15px 15px 20px -3px rgba(0, 0, 0, 0.125);
	}

	/* = Book Bone
-------------------------------------------------------------- */
	.book-bone {
		width: 50px;
		background: #4c7dfe;
		box-shadow:
			1px 0 0 #4c7dfe,
			-1px 0 0 #4c7dfe; /* 旋转的时候 拼接处隐隐约约会有个缝隙 所以加上个阴影来填补它 */
		position: absolute;
		top: 0;
		bottom: 16px;
		left: -25px;
		transform: rotate3d(0, 1, 0, -90deg);
	}

	.book-page,
	.book-top,
	.book-right,
	.book-bottom {
		background: var(--color-white);
	}

	.book-right {
		width: 49px;
		height: calc(100% - 1.5rem);
		position: absolute;
		top: 5px;
		right: -20px;
		box-shadow:
			0 1px 0 #eeefe9,
			0 -1px 0 #eeefe9;
		transform: rotate3d(0, 1, 0, 90deg);
	}
	.book-top {
		width: 100%;
		height: 50px;
		position: absolute;
		top: -20px;
		left: 0;
		transform: rotate3d(1, 0, 0, 90deg);
	}
	.book-bottom {
		width: 100%;
		height: 50px;
		position: absolute;
		bottom: -20px;
		left: 0;
		transform: rotate3d(1, 0, 0, -90deg) translate3d(0, 0, 0);
	}
	.book-right,
	.book-top,
	.book-bottom {
		backface-visibility: hidden;
	}

	/* MEDIA QUERIES */
	@media only screen and (min-width: 400px) and (min-height: 600px) {
		.book-cover .byline {
			font-size: var(--24px);
		}
	}
	@media only screen and (min-width: 600px) and (min-height: 800px) {
		.book-cover .byline {
			font-size: var(--40px);
			bottom: 1rem;
		}
		.book-cover-back-indent,
		.page {
			padding: 2rem;
		}
		.book-cover-back-indent p,
		#page-1 p,
		.book-page p {
			font-size: 16px;
		}
		:global(.initial-cap) {
			font-size: 60px;
			line-height: 0.8;
		}
	}
	@media only screen and (min-width: 800px) and (min-height: 1000px) {
		.book-cover h1 {
			margin: 0 auto;
		}
		.book-cover .byline {
			font-size: var(--44px);
			bottom: 1rem;
		}
	}
	@media only screen and (min-width: 1000px) and (min-height: 1200px) {
		.book-cover h1 {
			margin: -1rem auto 0 auto;
		}
		.book-cover .byline {
			font-size: var(--44px);
		}
	}
</style>
