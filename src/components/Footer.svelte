<footer>Made with ❤️ by Jums & Johnny</footer>

<style lang="scss">
    @import "../styles/vars";

    @font-face {
        font-family: "Product Sans";
        src: url("/fonts/product-sans/Product_Sans_Regular.ttf")
            format("truetype");
    }

    $mainFont: "Product Sans", sans-serif;

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
        font-family: $mainFont;
    }
</style>
