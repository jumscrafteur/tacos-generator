<script>
	import Header from "./components/Header.svelte";
	import Option from "./components/Option.svelte";
	import SizeSelect from "./components/SizeSelect.svelte";
	import ItemContainer from "./components/ItemContainer.svelte";
	import Footer from "./components/Footer.svelte";

	let optTaille = "M";
	let optDoublePoulet = false;
	let optTenders = false;
	let optFalafels = false;
	let optSupplements = 0;
	let nbSupplements;
	let tacos = { viandes: [], sauces: [], supplements: [] };
	let charQueue = [];

	let tailles = {
		M: 1,
		L: 2,
		XL: 3,
	};

	$: {
		tacos.viandes = choisirViandes(optTaille);
		tacos.sauces = choisirSauces();
		tacos.supplements = choisirSupplements(optSupplements);
	}

	let choisirViandes = (taille) => {
		let viandeChoisis = [];

		let viandes = [
			"Cordon bleu",
			"Nuggets",
			"Poulet nature",
			"Viande hachée",
			"Merguez",
		];

		if (optDoublePoulet) viandes.push("Poulet mariné");
		if (optTenders) viandes.push("Tenders");
		if (optFalafels) viandes.push("Falafels");

		for (let i = 0; i < tailles[taille]; i++) {
			let randomViande = Math.floor(Math.random() * viandes.length);
			viandeChoisis.push(viandes[randomViande]);
			viandes.splice(randomViande, 1);
		}

		return viandeChoisis;
	};

	let choisirSauces = () => {
		let saucesChoisis = [];

		let sauces = [
			"Algerienne",
			"Barbecue",
			"Biggy",
			"Chili-thai",
			"Curry",
			"Fuego",
			"Ketchup",
			"Mayonnaise",
			"Samourai",
		];

		for (let i = 0; i < 2; i++) {
			let randomSauce = Math.floor(Math.random() * sauces.length);
			saucesChoisis.push(sauces[randomSauce]);
			sauces.splice(randomSauce, 1);
		}

		return saucesChoisis;
	};

	let choisirSupplements = (nb) => {
		let supplementsChoisis = [];

		let supplements = [
			"Gouda",
			"Oignons",
			"Lardons",
			"Pastrami",
			"Poivronnade",
			"Vache qui rit",
			"Boursin",
			"Bacon",
			"Raclette",
			"Cheddar",
			"Chèvre",
			"Mozzarella",
			"Champignons",
			"Jalapeno",
		];

		nbSupplements = Math.max(nb, 0);
		nbSupplements = Math.min(nbSupplements, 14);

		for (let i = 0; i < nbSupplements; i++) {
			let random = Math.floor(Math.random() * supplements.length);
			supplementsChoisis.push(supplements[random]);
			supplements.splice(random, 1);
		}

		return supplementsChoisis;
	};

	let handleKeydown = (e) => {
		charQueue.push(e.key);
		if (charQueue.slice(-8).join("") == "pioupiou") {
			tacos.viandes = ["Nuggets"];
			tacos.sauces = ["Mayonnaise"];
		}
	};

	function refresh() {
		tacos.viandes = choisirViandes(optTaille);
		tacos.sauces = choisirSauces();
		tacos.supplements = choisirSupplements(optSupplements);
	}
</script>

<svelte:window on:keydown={handleKeydown} />

<Header />
<main>
	<div class="optBar">
		<div class="optItems">
			<Option
				checkbox={false}
				label={"Suppléments"}
				bind:value={optSupplements}
			/>
			<Option label={"Double poulet"} bind:value={optDoublePoulet} />
			<Option label={"Tenders"} bind:value={optTenders} />
			<Option label={"Falafels"} bind:value={optFalafels} />
		</div>

		<div class="icon">
			<img
				src="/images/save.svg"
				alt="save"
				class="icon disabled"
				height="16px"
			/>
			<img
				src="/images/refresh_arrow.svg"
				alt="refresh arrow"
				class="icon"
				height="20px"
				on:click={refresh}
			/>
		</div>
	</div>
	<h2>Tailles</h2>
	<div class="sizeBar">
		<SizeSelect sizes={["M", "L", "XL"]} bind:value={optTaille} />
	</div>
	<hr class="separator" />
	<ItemContainer Items={tacos.viandes} label={"Viande"} />
	<ItemContainer Items={tacos.sauces} label={"Sauce"} />

	{#if optSupplements > 0}
		<ItemContainer Items={tacos.supplements} label={"Supplement"} />
	{/if}
</main>
<Footer />

<style lang="scss">
	@import "./styles/vars";
	@import url("https://rsms.me/inter/inter.css");

	@font-face {
		font-family: "Product Sans";
		src: url("/fonts/product-sans/Product_Sans_Regular.ttf")
			format("truetype");
	}

	$mainFont: "Product Sans", sans-serif;

	* {
		font-family: $mainFont;
	}

	main {
		padding: 11.6px 11.6px 50px 11.6px;
		margin: 0 auto;
		width: clamp(100px, 600px, 100%);
		min-height: 100%;
	}

	.optBar {
		display: flex;
		flex-wrap: nowrap;

		& .optItems {
			padding: 10px 0;
			display: flex;

			overflow-x: auto;
			overflow-y: none;

			&::-webkit-scrollbar {
				width: 5px;
				height: 5px;
			}

			&::-webkit-scrollbar-track {
				box-shadow: inset 0 0 5px $soft;
				border-radius: 10px;
			}

			&::-webkit-scrollbar-thumb {
				background: $primary;
				border-radius: 999px;
			}
		}
		& .icon {
			margin: 0 0 0 auto;

			display: flex;
			align-items: center;

			& img {
				margin: 0 0 0 10px;
				cursor: pointer;
			}
		}
	}

	.sizeBar {
		color: $primary;
		margin: 21px 0;

		& .sizeItems {
			margin-top: 15.5px;
			display: flex;
		}
	}

	.separator {
		margin: 10px 0;
		width: 26px;
		border: 2px solid $primary;
		border-radius: 9999px;
	}

	h2 {
		margin: 16px 0;

		font-size: 22px;
		color: $primary;
		font-weight: light;
	}

	.disabled {
		opacity: 0.5;
	}
</style>
