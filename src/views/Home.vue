<template>
  <div class="home">
    <transition name="alert">
      <Alert v-if="showAlert" msg="Please add a todo..." />
    </transition>
    <AddTodo @noValue="errorTrigger" />
  </div>
</template>

<script>

import { ref } from 'vue'
import AddTodo from '@/components/AddTodo.vue'
import Alert from '../components/Alert.vue'

export default {
  components: { AddTodo, Alert },
  setup() {
    const showAlert = ref(false)

    const errorTrigger = () => {
      showAlert.value = true
      setTimeout(() => showAlert.value = false, 3000)
    }

    return { showAlert, errorTrigger }
  }
}
</script>

<style>
  /* .alert-enter-from {
    opacity: 0;
    transform: translateY(-60px);
  }
  .alert-enter-to {
    opacity: 1;
    transform: translateY(0);
  } */
  .alert-enter-active {
    /* transition: all 0.3s ease; */
    animation: wobble 0.5s ease;
  }
  .alert-leave-from {
    opacity: 1;
    transform: translateY(0);
  }
  .alert-leave-to {
    opacity: 0;
    transform: translateY(-60px);
  } 
  .alert-leave-active {
    transition: all 0.3s ease;
  }
  @keyframes wobble {
    0% { transform: translateY(-60px); opacity: 0; }
    50% { transform: translateY(0); opacity: 1; }
    60% { transform: translateX(8px); }
    70% { transform: translateX(-8px); }
    80% { transform: translateX(4px); }
    90% { transform: translateX(-4px); }
    100% { transform: translateX(0); }
  }
</style>