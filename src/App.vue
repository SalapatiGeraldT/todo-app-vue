<script setup>
import { RouterView } from 'vue-router';
import GlobalHeader from './components/GlobalHeader.vue';
</script>

<template>
  <GlobalHeader/>
  <RouterView />
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Mulish:wght@500;900&display=swap');
*{
  font-family: 'Mulish', sans-serif;
}
</style>
