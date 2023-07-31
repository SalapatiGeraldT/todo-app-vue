<template>
  <div>
      <!-- name="about" -->
  <transition 
  appear
  @before-enter="beforeEnter"
  @enter="enter"
  @after-enter="afterEnter"

  @after-leave="afterLeave"
  @leave="leave"
  @before-leave="beforeLeave"
  >
    <h1 v-if="title" class=" text-center ">May this be a start for a bigger project!</h1>
  </transition>
  <div class="text-center">
    <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s,</p>
    <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s,</p>
  </div>

  <transition name="fade">
    <div v-if="show">asdasd</div>
  </transition>

  <button @click="show = !show">click</button>
  </div>
</template>

<script setup>
import { ref } from "vue";
const show = ref(false);
const title = ref(true);

const beforeEnter = () => {
  console.log('before enter');
};

const enter = () => {
  console.log('enter');


};
const afterEnter = () => {
  console.log('after enter');
  setTimeout(() => title.value = false, 2000)
};
const beforeLeave = () => {
  console.log('before leave');

};

const leave = () => {
  console.log('leave');

};

const afterLeave = () => {
  console.log('after leave');

};




</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}

/* .about-enter-from {
  opacity: 0;
}

.about-enter-to {
  opacity: 1;
}

.about-enter-active {
  transition: all 2s ease;
}



.about-leave-to {
  opacity: 0;
}

.about-leave-active {
  transition: all 2s ease;
} */

.fade-leave-from {
}

.fade-leave-to {
}

.fade-leave-active {
}
</style>
