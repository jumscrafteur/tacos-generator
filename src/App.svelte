<script>
	let optTaille = "M";
	let optDoublePoulet = false;
	let optTenders = false;
	let optFalafels = false;
	let optSupplements = 0;
	let nbSupplements;
	let tacos = { viandes: [], sauces: [], supplements: [] };
	let charQueue = [];

	let url = {
		"Poulet nature": "chicken",
		"Poulet mariné": "chicken-marinated",
		"Viande hachée": "chopped-meat",
		Merguez: "sausage",
		Nuggets: "nuggets",
		"Cordon bleu": "cordon-blue",
		Tenders: "tenders",
		Falafels: "falafel",

		Algerienne: "algerian",
		Barbecue: "bbq",
		Biggy: "biggy",
		"Chili-thai": "thai-chili",
		Curry: "curry",
		Fuego: "fuego",
		Ketchup: "ketchup",
		Mayonnaise: "mayonnaise",
		Samourai: "samourai",

		Gouda: "gouda",
		Oignons: "caramelized-onions",
		Lardons: "chicken-bacon",
		Pastrami: "pastrami",
		Poivronnade: "paprika",
		"Vache qui rit": "vache-qui-rit",
		Boursin: "boursin",
		Bacon: "turkey-bacon",
		Raclette: "raclette",
		Cheddar: "cheddar",
		Chèvre: "goat-cheese",
		Mozzarella: "mozzarella",
		Champignons: "mushrooms",
		Jalapeno: "jalapeno-cheese",

		"Frit'OTacos": "fries-otacos",
		"Barquette de Frites ": "fries",

		"Coca-Cola": "coca-cola",
		Fanta: "fanta",
		Tropico: "tropico",
	};

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

	function handleClick() {
		tacos.viandes = choisirViandes(optTaille);
		tacos.sauces = choisirSauces();
		tacos.supplements = choisirSupplements(optSupplements);
	}
</script>

<svelte:window on:keydown={handleKeydown} />

<div class="header">
	<img src="/images/logo_text.svg" alt="" height="52px" class="logo" />
	<img src="/images/folder.svg" alt="" height="14px" class="icon disabled" />
</div>
<main>
	<div class="optBar">
		<div class="optItems">
			<div class="optItem">
				<label for="optSupplements">Suppléments</label><input
					id="optSupplements"
					type="number"
					min="0"
					max="14"
					bind:value={optSupplements}
				/>
			</div>
			<div class="optItem" class:selected={optDoublePoulet}>
				<input
					id="optDoublePoulet"
					type="checkbox"
					bind:checked={optDoublePoulet}
				/>
				<label for="optDoublePoulet">Double poulet </label>
			</div>
			<div class="optItem" class:selected={optTenders}>
				<input
					id="optTenders"
					type="checkbox"
					bind:checked={optTenders}
				/>
				<label for="optTenders">Tenders</label>
			</div>
			<div class="optItem" class:selected={optFalafels}>
				<input
					id="optFalafels"
					type="checkbox"
					bind:checked={optFalafels}
				/>
				<label for="optFalafels">Falafels</label>
			</div>
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
				on:click={handleClick}
			/>
		</div>
	</div>
	<h2>Tailles</h2>
	<div class="sizeBar">
		<div class="sizeItems">
			<div class="sizeItem" class:selected={optTaille == "M"}>
				<input type="radio" bind:group={optTaille} value={"M"} id="M" />
				<label for="M">M</label>
			</div>
			<div class="sizeItem" class:selected={optTaille == "L"}>
				<input type="radio" bind:group={optTaille} value={"L"} id="L" />
				<label for="L">L</label>
			</div>
			<div class="sizeItem" class:selected={optTaille == "XL"}>
				<input
					type="radio"
					bind:group={optTaille}
					value={"XL"}
					id="XL"
				/>
				<label for="XL">XL</label>
			</div>
		</div>
	</div>
	<hr class="separator" />
	<h2>
		Viande{#if optTaille != "M"}s{/if}
	</h2>
	<div class="contentBar">
		{#each tacos.viandes as viande}
			<div class="contentItem">
				<img
					src="https://o-tacos.com/soundboard/images/{url[
						viande
					]}_thumb.png"
					alt=""
				/>
				<p>{viande}</p>
			</div>
		{/each}
	</div>
	<h2>
		Sauce{#if optTaille != "M"}s{/if}
	</h2>
	<div class="contentBar">
		{#each tacos.sauces as sauce}
			<div class="contentItem">
				<img
					src="https://o-tacos.com/soundboard/images/{url[
						sauce
					]}_thumb.png"
					alt=""
				/>
				<p>{sauce}</p>
			</div>
		{/each}
	</div>
	{#if optSupplements > 0}
		<h2>
			Supplement{#if optSupplements > 1}s{/if}
		</h2>
		<div class="contentBar">
			{#each tacos.supplements as supplement}
				<div class="contentItem">
					<img
						src="https://o-tacos.com/soundboard/images/{url[
							supplement
						]}_thumb.png"
						alt=""
					/>
					<p>{supplement}</p>
				</div>
			{/each}
		</div>
	{/if}
</main>
<footer>Made with ❤️ by Jums & Johnny</footer>

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
	.header {
		width: 100%;
		height: 78px;

		background-color: $primary;
		box-shadow: 0px 2px 0px 0px rgba(29, 29, 27, 0.1);

		& .logo {
			position: relative;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
		}

		& .icon {
			position: relative;
			float: right;
			top: 50%;
			right: 14px;
			transform: translate(0, -50%);
		}
	}

	main {
		padding: 11.6px 11.6px 50px 11.6px;
		z-index: 0;
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

			& .optItem {
				display: flex;
				align-items: stretch;
				margin: 0 9.7px 0 0;
				border: 2px solid $primary;
				border-radius: 6.2px;

				& label {
					margin: 3px 6px;

					color: $primary;
					font-size: 12px;
					white-space: nowrap;
				}

				& input[type="number"] {
					// height: 27px;
					width: 21px;

					background-color: $primary;
					border: none;
					outline: none;

					color: $white;
					text-align: center;
				}
				& input[type="checkbox"] {
					display: none;
				}
				&.selected {
					background-color: $soft;
				}
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

			& .sizeItem {
				margin: 0 10px 0 0;
				height: 29px;
				width: 29px;

				display: flex;

				border: 2px solid $primary;
				border-radius: 4.5px;

				& input[type="radio"] {
					display: none;
				}

				& label {
					margin: auto;
				}

				&.selected {
					background-color: $soft;
				}
			}
		}
	}

	.contentBar {
		display: flex;

		overflow-x: auto;
		overflow-y: none;

		padding: 0 0 10px 0;

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

		& .contentItem {
			margin: 0 20px 0 0;
			width: 100px;
			height: 100px;

			display: flex;
			flex-direction: column;
			align-items: center;
			flex-shrink: 0;

			border: 2px solid $primary;
			border-radius: 7px;

			color: $primary;
			text-align: center;
			font-size: 14px;

			& img {
				margin-bottom: -6px;
				width: 80px;
				height: 80px;
			}
		}
	}

	.separator {
		margin: 10px 0;
		width: 26px;
		border: 2px solid $primary;
		border-radius: 9999px;
	}

	footer {
		position: absolute;
		bottom: 0;
		margin: 10px 0 0 0;
		height: 38px;
		width: 100%;

		display: flex;
		align-items: center;
		justify-content: center;

		color: $white;
		text-align: center;

		background-color: $primary;
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
