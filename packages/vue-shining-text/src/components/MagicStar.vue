<template>
    <span class="magic-star" :style="{
        top: `${top}%`,
        left: `${left}%`,
        fill: 'rgb(103, 58, 183)',
        scale,
    }" :class="{ blink }">
        <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 576 512">
            <path
                d="M316.9 18C311.6 7 300.4 0 288.1 0s-23.4 7-28.8 18L195 150.3 51.4 171.5c-12 1.8-22 10.2-25.7 21.7s-.7 24.2 7.9 32.7L137.8 329 113.2 474.7c-2 12 3 24.2 12.9 31.3s23 8 33.8 2.3l128.3-68.5 128.3 68.5c10.8 5.7 23.9 4.9 33.8-2.3s14.9-19.3 12.9-31.3L438.5 329 542.7 225.9c8.6-8.5 11.7-21.2 7.9-32.7s-13.7-19.9-25.7-21.7L381.2 150.3 316.9 18z" />
        </svg>
    </span>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';

const { delay } = defineProps<{
    delay: number
}>()


const rand = (min: number, max: number) => Math.floor(Math.random() * (max - min + 1)) + min

const blink = ref(false)
const top = ref(rand(-40, 100))
const left = ref(rand(-10, 100))
const scale = ref(0)

onMounted(() => {
    setTimeout(() => {
        blink.value = true
        scale.value = 1
        setInterval(() => {
            top.value = rand(-40, 100)
            left.value = rand(-10, 100)

        }, 1000);
    }, delay);

})

</script>


<style scoped>
@keyframes rotate {
    from {
        transform: rotate(0deg);
    }

    to {
        transform: rotate(180deg);
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

.blink {
    animation: scale 1000ms ease infinite;
}

.magic-star {
    position: absolute;
}

.magic-star>svg {
    animation: rotate 1000ms linear infinite;
    display: block;
    opacity: 0.7;
}
</style>
