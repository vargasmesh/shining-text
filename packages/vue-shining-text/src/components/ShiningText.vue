<template>
    <span class="magic">
        <span class="magic-star">
            <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 576 512">
                <path
                    d="M316.9 18C311.6 7 300.4 0 288.1 0s-23.4 7-28.8 18L195 150.3 51.4 171.5c-12 1.8-22 10.2-25.7 21.7s-.7 24.2 7.9 32.7L137.8 329 113.2 474.7c-2 12 3 24.2 12.9 31.3s23 8 33.8 2.3l128.3-68.5 128.3 68.5c10.8 5.7 23.9 4.9 33.8-2.3s14.9-19.3 12.9-31.3L438.5 329 542.7 225.9c8.6-8.5 11.7-21.2 7.9-32.7s-13.7-19.9-25.7-21.7L381.2 150.3 316.9 18z" />
            </svg>
        </span>
        <span class="magic-star">
            <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 576 512">
                <path
                    d="M316.9 18C311.6 7 300.4 0 288.1 0s-23.4 7-28.8 18L195 150.3 51.4 171.5c-12 1.8-22 10.2-25.7 21.7s-.7 24.2 7.9 32.7L137.8 329 113.2 474.7c-2 12 3 24.2 12.9 31.3s23 8 33.8 2.3l128.3-68.5 128.3 68.5c10.8 5.7 23.9 4.9 33.8-2.3s14.9-19.3 12.9-31.3L438.5 329 542.7 225.9c8.6-8.5 11.7-21.2 7.9-32.7s-13.7-19.9-25.7-21.7L381.2 150.3 316.9 18z" />
            </svg>
        </span>
        <span class="magic-star">
            <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 576 512">
                <path
                    d="M316.9 18C311.6 7 300.4 0 288.1 0s-23.4 7-28.8 18L195 150.3 51.4 171.5c-12 1.8-22 10.2-25.7 21.7s-.7 24.2 7.9 32.7L137.8 329 113.2 474.7c-2 12 3 24.2 12.9 31.3s23 8 33.8 2.3l128.3-68.5 128.3 68.5c10.8 5.7 23.9 4.9 33.8-2.3s14.9-19.3 12.9-31.3L438.5 329 542.7 225.9c8.6-8.5 11.7-21.2 7.9-32.7s-13.7-19.9-25.7-21.7L381.2 150.3 316.9 18z" />
            </svg>
        </span>
        <span class="magic-text">
            <slot />
        </span>
    </span>
</template>

<script lang="ts" setup>
import { onMounted } from 'vue';

const rand = (min: number, max: number) => Math.floor(Math.random() * (max - min + 1)) + min

const animate = (star: HTMLElement) => {
    star.style.setProperty("--star-left", `${rand(-10, 100)}%`);
    star.style.setProperty("--star-top", `${rand(-40, 100)}%`);
    star.style.animation = "none";
    star.offsetHeight;
    star.style.animation = "";
}

let index = 0,
    interval = 1000


onMounted(() => {
    for (const star of document.querySelectorAll<HTMLElement>(".magic-star")) {
        setTimeout(() => {
            animate(star);
            setInterval(() => animate(star), 1000);
        }, index++ * (interval / 3))
    }
})

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

@keyframes scale {

    from,
    to {
        transform: scale(0);
    }

    50% {
        transform: scale(1);
    }
}

@keyframes rotate {
    from {
        transform: rotate(0deg);
    }

    to {
        transform: rotate(180deg);
    }
}

.magic {
    display: inline-block;
    position: relative;
}

.magic>.magic-star {
    --size: clamp(20px, 1.5vw, 30px);

    animation: scale 700ms ease forwards;

    display: block;
    height: var(--size);
    left: var(--star-left);
    top: var(--star-top);
    position: absolute;
    width: var(--size);
}

.magic>.magic-star>svg {
    animation: rotate 1000ms linear infinite;
    display: block;
    opacity: 0.7;
}

.magic>.magic-star>svg>path {
    --violet: rgb(103, 58, 183);
    fill: var(--violet);
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
