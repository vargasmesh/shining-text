<template>
    <span>
        <slot />
    </span>
</template>

<style scoped>
@keyframes background-pan {
    from {
        background-position: 0% center;
    }

    to {
        background-position: -200% center;
    }
}


span {
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
