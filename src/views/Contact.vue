<template>
  <div>
    <h1>Contact</h1>
    <transition-group 
      appear
      tag="ul"
      @before-enter="beforeEnter"
      @enter="enter"
    >
      <li v-for="(icon, idx) in icons" :key="icon.name" :data-idx="idx">
        <span class="material-icons">{{ icon.name }}</span>
        <div>{{ icon.text }}</div>
      </li>
    </transition-group>
  </div>
</template>

<script>
import { ref } from 'vue'
import gsap from 'gsap'

export default {
  setup() {
    const icons = ref([
      { name: 'alternate_email', text: 'by email' },
      { name: 'local_phone', text: 'by phone' },
      { name: 'local_post_office', text: 'by post' },
      { name: 'local_fire_department', text: 'by smoke signal' },
    ])

    const beforeEnter = (el) => {
      el.style.opacity = 0
      el.style.transform = 'translateY(100px)'
    }
    const enter = (el, done) => {
      gsap.to(el, {
        opacity: 1,
        y: 0,
        duration: 0.8,
        onComplete: done,
        delay: el.dataset.idx * 0.2,
      })
    }

    return { beforeEnter, enter, icons }
  }
}
</script>

<style scoped>
  h1 {
    margin-bottom: 20px;
  }
  ul{
    width: 300px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
  }
  li {
    list-style-type: none;
    background: #ddd;
    padding: 15px;
  }
</style>
