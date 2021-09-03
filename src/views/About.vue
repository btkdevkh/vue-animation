<template>
  <div class="about">
    <transition 
      appear
      @before-enter="beforeEnter"
      @enter="enter"
    >
      <h1>About</h1>
    </transition>
    <p>A simple app todos with VueJS</p>
  </div>
</template>

<script>
import gsap from 'gsap'

export default {
  setup() {
    const beforeEnter = (el) => {
      el.style.transform = 'translateY(-60px)'
      el.style.opacity = 0
    }
    const enter = (el, done) => {
      gsap.to(el, {
        opacity: 1,
        y: 0,
        duration: 1,
        ease: 'bounce.out',
        onComplete: done,
      })
    }

    return { beforeEnter, enter }
  }
}
</script>

<style>
</style>
