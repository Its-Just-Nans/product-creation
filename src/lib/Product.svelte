<script lang="ts">
    import Input from "./Input.svelte";
    import Map from "./Map.svelte";
    import { product, mergeDeep } from "../store";
    import Infos from "./Infos.svelte";
    window.addEventListener("load", () => {
        const savedProduct = localStorage.getItem("product");
        if (savedProduct) {
            const parsedProduct = JSON.parse(savedProduct);
            product.set(mergeDeep($product, parsedProduct));
        }
        product.subscribe((value) => {
            localStorage.setItem("product", JSON.stringify(value));
        });
    });
</script>

<div class="block noborder">
    <div class="flex1">
        <Input bind:input={$product.isFound} />
    </div>
</div>
{#if $product.isFound.value !== ""}
    {#if $product.isFound.value == "true"}
        <div class="block noborder">
            <div class="flex1">
                <Input bind:input={$product.name} />
            </div>
        </div>

        <div class="block noborder">
            <div class="flex1">
                <Input bind:input={$product.isVirtual} />
            </div>
        </div>
        {#if $product.isVirtual.value !== ""}
            <div class="block flex1 align last">
                {#if $product.isVirtual.value === "true"}
                    <div class="flex1 bright">
                        <h2 class="wei">Virtual product</h2>
                    </div>
                {:else if $product.isVirtual.value === "false"}
                    <div class="flex1 bright">
                        <div class="block">
                            <p class="wei">Physical product</p>
                        </div>
                        <div class="block col">
                            <p>Product location</p>
                            <Map />
                        </div>
                    </div>
                    <div class="block noborder vertical last">
                        {#each Object.keys($product.physical) as key}
                            <Input bind:input={$product.physical[key]} />
                        {/each}
                    </div>
                {/if}
            </div>
        {/if}
        <div class="block">
            <h3>Cost</h3>

            <div class="block noborder vertical last">
                <Input bind:input={$product.subscription} />
                <Input bind:input={$product.price} />
            </div>
        </div>
        <div class="block last">
            <h3>Around the product</h3>
            <div class="block noborder vertical last">
                {#each Object.keys($product.arroundProduct) as key}
                    <Input bind:input={$product.arroundProduct[key]} />
                {/each}
            </div>
        </div>
        <div class="block">
            <h3>Real life usage</h3>
            <div class="block noborder vertical last">
                {#each Object.keys($product.realLife) as key}
                    <Input bind:input={$product.realLife[key]} />
                {/each}
            </div>
        </div>

        <div class="block">
            <h3>Design</h3>

            <div class="block noborder vertical last">
                {#each Object.keys($product.design) as key}
                    <Input bind:input={$product.design[key]} />
                {/each}
            </div>
        </div>
        <div class="block">
            <h3>Product evaluation</h3>
            <div class="block noborder vertical last">
                {#each Object.keys($product.product) as key}
                    <Input bind:input={$product.product[key]} />
                {/each}
            </div>
        </div>
    {:else}
        <div class="block vertical noborder">
            <h2>Finding your Product</h2>
            <div class="block vertical noborder">
                {#each Object.keys($product.findingProduct) as key}
                    <Input bind:input={$product.findingProduct[key]} />
                {/each}
            </div>
            <div class="vertical">
                <Infos data={$product.wwwwwh} tag="h3" />
                <div class="block last noborder">
                    {#each Object.keys($product.wwwwwh) as key}
                        {#if typeof $product.wwwwwh[key] === "object"}
                            <div>
                                <Input bind:input={$product.wwwwwh[key]} />
                            </div>
                        {/if}
                    {/each}
                </div>
            </div>
        </div>
    {/if}
{/if}
