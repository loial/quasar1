<template>
  <q-page class="flex flex-center">
    <transition
    >
    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-vertical.svg"
      style="width: 200px; height: 200px"
      @click="animate"
      :data-animation="'flipOutY'"
    >
    </transition>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
const animateCSS =  (element,animation) =>
  // We create a Promise and return it
  new Promise((resolve, reject) => {

    element.classList.add('animate', animation);

    // When the animation ends, we clean the classes and resolve the Promise
    function handleAnimationEnd(event) {
      event.stopPropagation();
      event.target.classList.remove('animate', animation);
      resolve('Animation ended');
    }

    element.addEventListener('animationend', handleAnimationEnd, {once: true});
  });
export default defineComponent({
  name: 'IndexPage',
  methods: {
    animate(event) {
      let element=event.target
      console.log(element)
      let animation=element.getAttribute('data-animation');

      animateCSS(element,animation);
      }
  }
})
</script>
<style>
img {
  --animate-duration: 2s;
}
</style>
