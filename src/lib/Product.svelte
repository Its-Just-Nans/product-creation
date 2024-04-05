<script lang="ts">
    import Input from "./Input.svelte";
    import Map from "./Map.svelte";
    let product = {
        name: {
            type: "text",
            question: "What is the name of this product?",
            name: "name",
            value: "",
        },
        isVirtual: {
            type: "radio",
            question: "Is this a virtual product? (app, website, etc.)",
            name: "virtual-product",
            value: "",
        },
        physical: {
            safeChildren: {
                type: "radio",
                question: "Does this product contain small parts?",
                name: "safe-children",
            },
            healthRealted: {
                type: "radio",
                question: "Is this product health-related?",
                name: "health-related",
            },
            biodegradable: {
                type: "radio",
                question: "Is this product biodegradable?",
                name: "biodegradable",
            },
            electronics: {
                type: "radio",
                question: "Is this product an electronic device?",
                name: "electronics",
            },
        },
        sustainable: {
            type: "radio",
            question: "Is this product sustainable?",
            name: "sustainable",
        },
        recyclable: {
            type: "radio",
            question: "Is this product recyclable?",
            name: "recyclable",
        },
        behaviourChange: {
            type: "radio",
            question: "Does this product aim to change behaviour?",
            name: "behaviour-change",
        },
        emotional: {
            type: "radio",
            question: "Does this product aim to evoke an emotional response?",
            name: "emotional",
        },
        majority: {
            type: "radio",
            question: "Is this product aimed at the majority?",
            name: "majority",
        },
        cultureSensitive: {
            type: "radio",
            question: "Is this product sensitive to culture?",
            name: "culture-sensitive",
        },
        nonHuman: {
            type: "radio",
            question: "Is this product non-human?",
            name: "non-human",
        },
        subscription: {
            type: "radio",
            question: "Is this product a subscription?",
            name: "subscription",
        },
        price: {
            type: "text",
            question: "What is the cost of this product?",
            name: "price",
            value: "",
        },
    };
</script>

<div class="block">
    <div class="flex1">
        <Input bind:input={product.name} />
    </div>
</div>
<div class="block">
    <div class="flex1">
        <Input bind:input={product.isVirtual} />
    </div>
</div>
{#if product.isVirtual.value !== ""}
    <div class="block flex1 align">
        {#if product.isVirtual.value === "true"}
            <div class="flex1 bright">
                <p class="wei">Virtual product</p>
                <p>qsdf</p>
            </div>
        {:else if product.isVirtual.value === "false"}
            <div class="flex1 bright">
                <div class="block">
                    <p class="wei">Physical product</p>
                </div>
                <div class="block col">
                    <p>Product location</p>
                    <Map />
                </div>
                <div class="block col">
                    <p>Cost</p>
                    <div>
                        <Input bind:input={product.subscription} />
                        <Input bind:input={product.price} />
                    </div>
                </div>
            </div>
            <div>
                {#each Object.keys(product.physical) as key}
                    <div>
                        <Input bind:input={product.physical[key]} />
                    </div>
                {/each}
            </div>
        {/if}
    </div>
{/if}
