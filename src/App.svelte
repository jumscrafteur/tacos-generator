<script>
	let showMenu = true;
	let optTaille = "M";
	let optDoublePoulet = false;
	let optTenders = false;
	let optSupplements = 0;
	let nbSupplements;
	let tacos = { viandes: [], sauces: [], supplements: [] };

	let url = {
		"Cordon bleu": "cordon-blue",
		Nuggets: "nuggets",
		"Filet de poulet mariné": "chicken-marinated",
		"Filet de poulet nature": "chicken",
		Tenders: "tenders",
		"Viande hachée": "chopped-meat",
		Merguez: "sausage",
		Falafels: "falafel",

		Ketchup: "ketchup",
		Algerienne: "algerian",
		Barbecue: "bbq",
		Biggy: "biggy",
		Andalouse: "andalouse",
		"Chili-thai": "thai-chili",
		Mayonnaise: "mayonnaise",
		Samourai: "samourai",
		Harissa: "harissa",
		Curry: "curry",
		Fuego: "fuego",
		Tabasco: "tabasco",
		"Texane Pepper": "texane-pepper",

		Gouda: "gouda",
		"Oignons caramélisés": "caramelized-onions",
		"Lardons de volaille": "chicken-bacon",
		Pastrami: "pastrami",
		Poivronnade: "paprika",
		"Vache qui rit": "vache-qui-rit",
		Boursin: "boursin",
		"Bacon de dinde": "turkey-bacon",
		Raclette: "raclette",
		Cheddar: "cheddar",
		Chèvre: "goat-cheese",
		Mozzarella: "mozzarella",
		Champignons: "mushrooms",
		"Jalapeno et cheese nuggets": "jalapeno-cheese",

		"Frit'OTacos": "fries-otacos",
		"Barquette de Frites ": "fries",

		"Coca-Cola": "coca-cola",
		Fanta: "fanta",
		Tropico: "tropico",
	};
	$: {
		let tailles = {
			M: 1,
			L: 2,
			XL: 3,
		};

		let viandeChoisis = [];
		let saucesChoisis = [];

		let viandes = [
			"Cordon bleu",
			"Nuggets",
			"Filet de poulet nature",
			"Viande hachée",
			"Merguez",
			"Falafels",
		];

		let sauces = [
			"Ketchup",
			"Algerienne",
			"Barbecue",
			"Biggy",
			"Andalouse",
			"Chili-thai",
			"Mayonnaise",
			"Samourai",
			"Harissa",
			"Curry",
			"Fuego",
			"Tabasco",
			"Texane Pepper",
		];

		if (optDoublePoulet) viandes.push("Filet de poulet mariné");
		if (optTenders) viandes.push("Tenders");

		for (let i = 0; i < tailles[optTaille]; i++) {
			let randomViande = Math.floor(Math.random() * viandes.length);
			viandeChoisis.push(viandes[randomViande]);
			viandes.splice(randomViande, 1);

			let randomSauce = Math.floor(Math.random() * sauces.length);
			saucesChoisis.push(sauces[randomSauce]);
			sauces.splice(randomSauce, 1);
		}

		tacos.viandes = viandeChoisis;
		tacos.sauces = saucesChoisis;
	}
	$: {
		let supplementsChoisis = [];

		let supplements = [
			"Gouda",
			"Oignons caramélisés",
			"Lardons de volaille",
			"Pastrami",
			"Poivronnade",
			"Vache qui rit",
			"Boursin",
			"Bacon de dinde",
			"Raclette",
			"Cheddar",
			"Chèvre",
			"Mozzarella",
			"Champignons",
			"Jalapeno et cheese nuggets",
		];

		nbSupplements = Math.max(optSupplements, 0);
		nbSupplements = Math.min(nbSupplements, 14);

		for (let i = 0; i < nbSupplements; i++) {
			let random = Math.floor(Math.random() * supplements.length);
			supplementsChoisis.push(supplements[random]);
			supplements.splice(random, 1);
		}

		tacos.supplements = supplementsChoisis;
	}
</script>

<div class="sidebar">
	<input
		type="checkbox"
		name="show_menu"
		id="show_menu"
		bind:checked={showMenu}
	/><label for="show_menu" class="menuToggle">Afficher les options</label>
	<form class:hidden={!showMenu} on:submit|preventDefault>
		<fieldset>
			<legend>Taille</legend>
			<div class="input-group checkbox">
				<input type="radio" bind:group={optTaille} value={"M"} id="M" />
				<label for="M">M</label>
				<input type="radio" bind:group={optTaille} value={"L"} id="L" />
				<label for="L">L</label>
				<input
					type="radio"
					bind:group={optTaille}
					value={"XL"}
					id="XL"
				/>
				<label for="XL">XL</label>
			</div>
		</fieldset>
		<fieldset class="vertical">
			<legend>Options</legend>

			<div class="input-group checkbox">
				<input
					type="checkbox"
					name="option_double_poulet"
					id="option_double_poulet"
					bind:checked={optDoublePoulet}
				/><label for="option_double_poulet">Double Poulet</label>
				<input
					type="checkbox"
					name="option_tenders"
					id="option_tenders"
					bind:checked={optTenders}
				/><label for="option_tenders">Tenders</label>
			</div>
			<div class="input-group number">
				<label for="option_supplements">Suppléments :</label><input
					type="number"
					name="option_supplements"
					id="option_supplements"
					min="0"
					max="14"
					bind:value={optSupplements}
				/>
			</div>
		</fieldset>
	</form>
</div>
<main>
	<h2>Taille</h2>
	<div class="badge"><p>{optTaille}</p></div>
	<h2>
		Viande{#if optTaille != "M"}s{/if}
	</h2>
	<div class="badgeHolder">
		{#each tacos.viandes as viande}
			<div class="badge">
				<p>
					<img
						src="https://o-tacos.com/soundboard/images/{url[
							viande
						]}_thumb.png"
						alt=""
					/> <br />
					{viande}
				</p>
			</div>
		{/each}
	</div>
	<h2>
		Sauce{#if optTaille != "M"}s{/if}
	</h2>
	<div class="badgeHolder">
		{#each tacos.sauces as sauce}
			<div class="badge">
				<p>
					<img
						src="https://o-tacos.com/soundboard/images/{url[
							sauce
						]}_thumb.png"
						alt=""
					/> <br />
					{sauce}
				</p>
			</div>
		{/each}
	</div>
	{#if optSupplements > 0}
		<h2>
			Supplement{#if optSupplements > 1}s{/if}
		</h2>
	{/if}
	<div class="badgeHolder">
		{#each tacos.supplements as supplement}
			<div class="badge">
				<p>
					<img
						src="https://o-tacos.com/soundboard/images/{url[
							supplement
						]}_thumb.png"
						alt=""
					/> <br />
					{supplement}
				</p>
			</div>
		{/each}
	</div>
</main>

<style lang="scss">
	.sidebar {
		padding: 20px 10px;
		font-family: Unica One, sans-serif;
		color: white;
		background-color: #2a2c31;
		display: flex;
		flex-direction: column;
	}

	.hidden {
		display: none;
	}

	.vertical {
		display: flex;
		flex-direction: column;
	}

	fieldset {
		padding: 0 20px;
		margin: 0 0 10px 0;
		border: none;
	}

	legend {
		text-align: center;
	}

	.input-group {
		margin: 7px 0 0 0;
		padding: 5px 10px;
		// margin: inherit auto;
		box-sizing: unset;

		border-radius: 5px;
		border: 1px solid white;

		background-color: white;
		color: black;

		display: flex;
		&.checkbox {
			justify-content: space-evenly;
		}
		&.number {
			justify-content: center;
			& input {
				border: none;

				text-align: center;
				font-family: Unica One, sans-serif;
			}
		}
	}

	input[type="radio"],
	input[type="checkbox"] {
		display: none;

		& + label {
			padding: 5px 10px;

			border-radius: 5px;
			border: 1px solid white;

			background-color: white;
			color: black;
		}

		&:checked + label {
			border: 1px solid #e54315;

			color: #e54315;
		}
	}

	input[type="checkbox"] {
		&:checked + label::before {
			content: "👍";
		}

		&:not(:checked) + label::before {
			content: "👎";
		}
	}

	main {
		height: 100%;

		background-color: #290f1c;

		color: white;
		font-family: Unica One, sans-serif;
		text-align: center;

		display: flex;
		flex-direction: column;
		align-items: center;

		& h2 {
			margin: 5px;
		}

		& .badge p {
			padding: 5px 10px;

			color: #e54315;
			font-weight: bolder;
			font-size: 24px;

			background-color: white;

			border-radius: 10px;
			border: 1px solid #e54315;
		}

		& .badgeHolder .badge:not(:first-child) {
			margin: 5px 0 0 0;
		}
	}

	@media screen and (min-width: 700px) {
		.sidebar {
			flex-direction: row;
			align-items: flex-start;
			& form {
				flex-grow: 4;
			}
		}
	}
</style>
