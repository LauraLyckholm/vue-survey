<script setup>

const props = defineProps({
    heroText: String
});
console.log(props.heroText);
</script>

<template>
    <section>
        <h1>{{ props.heroText }}</h1>
    </section>
</template>

<style lang="scss" scoped>
section {
    height: 300px;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background: url('~/assets/hero-banner.jpg') no-repeat center center;

    @media (min-width: 768px) {
        height: 400px;
    }

    h1 {
        color: white;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
        font-size: 2rem;
        font-weight: 900;
        text-transform: uppercase;

        @media (min-width: 768px) {
            font-size: 4rem;
        }
    }
}
</style>