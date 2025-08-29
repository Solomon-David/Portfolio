<script setup>
    const props = defineProps ({
        colorscheme: {
            type: String,
            default: "var(--primary)"
        },

        subtitle: {
            type: String,
            required: false
        },

        subcolor: {
            type: String,
            default: "var(--color)"
        }
    })
</script>    

<template>
    <div class="section-heading">
        <h2 :style="{color: props.colorscheme}" > <slot></slot> </h2>
        <p class="subtitle" :style="{color: props.subcolor}"> {{subtitle ?? ""}} </p>
        
    </div>
</template>

<style scoped>
    .section-heading {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
        gap: 1.5rem;
    }

    .section-heading h2 {
        font-size: calc(var(--heading-size)*1.3);
        font-weight: 700;
        font-family: var(--heading-font);
        text-transform: capitalize;
        position:relative;
    }

    .section-heading h2::after {
        content: "";
        position: absolute;
        width: 80%;
        bottom: -0.5rem;
        left: 10%;
        border-bottom: 3px solid;
    }

    .subtitle {
        font-size: calc(var(--body-size) * 0.9);
        max-width: 70vw;
    }

</style>