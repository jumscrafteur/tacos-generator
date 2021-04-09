<script>
    import Item from "./Item.svelte";

    export let Items;
    export let label;
</script>

<h2>
    {label}{#if Items.length > 1}s{/if}
</h2>
<div class="contentBar">
    {#each Items as item}
        <Item content={item} />
    {/each}
</div>

<style lang="scss">
    @import "../styles/vars";

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
    }

    h2 {
        margin: 16px 0;

        font-size: 22px;
        color: $primary;
        font-weight: light;
    }
</style>
