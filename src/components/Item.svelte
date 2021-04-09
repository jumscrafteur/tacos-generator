<script>
    export let content;
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
</script>

<div class="contentItem">
    <img
        src="https://o-tacos.com/soundboard/images/{url[content]}_thumb.png"
        alt=""
    />
    <p>{content}</p>
</div>

<style lang="scss">
    @import "../styles/vars";

    .contentItem {
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
</style>
