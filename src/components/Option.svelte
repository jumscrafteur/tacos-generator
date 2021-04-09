<script>
    export let value = 0;
    export let checkbox = true;
    export let label = "Option";

    let labelId = label.replace(" ", "");
</script>

<div class="optItem" class:selected={value === true}>
    <label for={label}>{label}</label>
    {#if checkbox}
        <input id={label} type="checkbox" bind:checked={value} />
    {:else}
        <input id={label} type="number" min="0" max="14" bind:value />
    {/if}
</div>

<style lang="scss">
    @import "../styles/vars";
    .optItem {
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
            width: 21px;

            background-color: $primary;
            border: none;
            outline: none;

            color: $white;
            text-align: center;

            -moz-appearance: textfield;

            /* Chrome */
            &::-webkit-inner-spin-button {
                -webkit-appearance: none;
                margin: 0;
            }

            /* Opéra*/
            &::-o-inner-spin-button {
                -o-appearance: none;
                margin: 0;
            }
        }
        & input[type="checkbox"] {
            display: none;
        }
        &.selected {
            background-color: $soft;
        }
    }
</style>
