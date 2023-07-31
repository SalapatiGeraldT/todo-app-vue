<script setup>
import { RouterView } from 'vue-router';
import GlobalHeader from './components/GlobalHeader.vue';
</script>

<template>
 <div>
    <GlobalHeader/>
  
    <!-- <transition name="route" mode="out-in">
      <RouterView />
    </transition> -->
    <router-view v-slot="{ Component }">
  <transition name="route" mode="out-in">
    <component :is="Component" />
  </transition>
</router-view>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Mulish:wght@500;900&display=swap');
*{
  font-family: 'Mulish', sans-serif;
}

.route-enter-from{
  opacity: 0;
  transform: translateX(100px);
}
.route-enter-active{
  transition: all 0.3s ease-out;
}

.route-leave-to{
  opacity: 0;
  transform: translateX(-100px);

}
.route-leave-active{
  transition: all 0.3s ease-in;
}


</style>
