<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';
import QuestionCard from '~/components/QuestionCard.vue';
import HeroBanner from '~/components/HeroBanner.vue';

// const windowWidth = ref(window.innerWidth);

// const handleResize = () => { windowWidth.value = window.innerWidth; };
// onMounted(() => window.addEventListener('resize', handleResize));
// onUnmounted(() => window.removeEventListener('resize', handleResize));

// const longHeroText = 'My first Vue Survey';
// const shortHeroText = 'Vue Survey';

// const heroText = computed(() => windowWidth.value > 600 ? longHeroText : shortHeroText);

const heroText = 'Vue Survey';
</script>

<template>
  <section>
    <HeroBanner :heroText="heroText" />
    <QuestionCard />
  </section>
</template>

<style lang="scss">
section {
  margin: 0 auto;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}
</style>