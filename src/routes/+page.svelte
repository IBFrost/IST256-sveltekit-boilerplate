<script>
	import Counter from './Counter.svelte';
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcome_fallback from '$lib/images/svelte-welcome.png';
	import { onMount } from 'svelte';

	onMount(() => {
		function duplicateCard() {
			var card = document.querySelector('#cardContainer');
			var cardClone = card.cloneNode(true);
			card.parentNode.appendChild(cardClone);
		}

		function colorChange() {
			var cards = document.querySelectorAll('#cardContainer');
			var newColor = '#' + Math.floor(Math.random() * 16777215).toString(16);
			for (const e of cards) {
				e.style.backgroundColor = newColor;
			}
		}

		function deleteLast() {
			const cards = document.querySelectorAll('#cardContainer');
			if (cards.length > 1) {
				cards[cards.length - 1].parentNode.removeChild(cards[cards.length - 1]);
			}
		}

		function headingChange() {
			var cards = document.querySelectorAll('#title');
			for (const e of cards) {
				e.textContent = 'something else';
			}
		}

		var duplicator = document.querySelector('#duplicate');
		duplicate.addEventListener('click', duplicateCard);

		var colorChanger = document.querySelector('#colorChange');
		colorChanger.addEventListener('click', colorChange);

		var headingChanger = document.querySelector('#headingChange');
		headingChanger.addEventListener('click', headingChange);

		var deleteButton = document.querySelector('#deleteLast');
		deleteButton.addEventListener('click', deleteLast);
	});
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		<span class="welcome">
			<picture>
				<source srcset={welcome} type="image/webp" />
				<img src={welcome_fallback} alt="Welcome" />
			</picture>
		</span>

		to your new<br />SvelteKit app
	</h1>

	<h2>
		try editing <strong>src/routes/+page.svelte</strong>
	</h2>

	<Counter />
</section>

<section>
	<div class="wrapper">
		<button id="duplicate"> Duplicate Card </button>
		<button id="colorChange"> Change Color </button>
		<button id="headingChange"> Change Heading </button>
		<button id="deleteLast"> Delete Last </button>
		<div id="cardContainer">
			<div>
				<h1 id="title">Gotem</h1>
			</div>
			<img
				id="cardImg"
				src="https://i.kym-cdn.com/photos/images/newsfeed/001/323/085/7fd.jpg"
				alt="Circle Game. You lose."
			/>
			<details>
				<summary>Details</summary>
				<p>Image deviously licked from KnowYourMeme</p>
			</details>
		</div>
	</div>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}

	button {
		visibility: visible;
		margin: 8px;
	}
	#cardContainer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: flex;
		border: solid 8px;
		border-color: black;
		max-width: 400px;
		background-color: #5c4033;
		color: white;
		margin: 8px;
	}
	h1 {
		font-family: Arial;
		text-align: center;
		margin: 8px;
	}
	a {
		margin: auto;
		width: 100px;
	}
	#cardImg {
		margin: 16px;
		margin-bottom: 0;
		max-width: 400px;
	}
	p {
		font-family: Arial;
		margin-left: 16px;
		max-width: 400px;
	}
	details {
		font-family: Arial;
		margin-left: 16px;
		max-width: 400px;
	}
	@media screen and (max-width: 800px) and (min-width: 500px) {
		button {
			visibility: visible;
		}
	}
	@media screen and (max-width: 500px) {
		#cardContainer {
			max-width: 90%;
		}
	}
</style>
