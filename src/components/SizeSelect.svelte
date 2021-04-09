<script>
    export let sizes = ["S"];
    export let value;
    let optTaille;
</script>

<div class="sizeItems">
    {#each sizes as size}
        <div class="sizeItem" class:selected={value == size}>
            <input type="radio" bind:group={value} value={size} id={size} />
            <label for={size}>{size}</label>
        </div>
    {/each}
</div>

<style lang="scss">
    @import "../styles/vars";

    .sizeItems {
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
</style>
