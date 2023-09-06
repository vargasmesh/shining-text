<template>
    <span class="magic">
        <MagicStar :delay=300 />
        <MagicStar :delay=600 />
        <MagicStar :delay=900 />
        <span class="magic-text">
            <slot />
        </span>
    </span>
</template>

<script lang="ts" setup>
import MagicStar from "./MagicStar.vue"

</script>



<style scoped>
@keyframes background-pan {
    from {
        background-position: 0% center;
    }

    to {
        background-position: -200% center;
    }
}

.magic {
    display: inline-block;
    position: relative;
}

.magic>.magic-text {
    color: white;
    font-size: 4rem;

    --purple: rgb(123, 31, 162);
    --violet: rgb(103, 58, 183);
    --pink: rgb(244, 143, 177);

    background: linear-gradient(to right,
            var(--purple),
            var(--violet),
            var(--pink),
            var(--purple));
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    white-space: nowrap;

    background-size: 200%;
    animation: background-pan 3s linear infinite;
}
</style>
