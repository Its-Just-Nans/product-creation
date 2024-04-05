<script lang="ts">
    import DesignThinking from "./lib/DesignThinking.svelte";
    import Product from "./lib/Product.svelte";
</script>

<main class="col">
    <div class="block">
        <p class="title">product creation</p>
    </div>

    <div>
        <Product />
    </div>
    <div>
        <DesignThinking />
    </div>
</main>

<style>
    p {
        text-transform: uppercase;
        font-weight: bolder;
        margin: 0px;
        font-size: 1.5em;
        text-align: center;
        padding: 10px;
        word-spacing: 30px;
        letter-spacing: 10px;
    }
</style>
