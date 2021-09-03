<template>
  <div>
    <h1>Todo</h1>
    <input 
      @keypress.enter="addTodo"
      type="text"
      v-model="newTodo"
      placeholder="add todo..."
    />
  </div>

  <transition name="switch" mode="out-in">
    <div v-if="todos.length">
      <transition-group tag="ul" name="list" appear>
        <li v-for="todo in todos" @click="deleteTodo(todo.id)" :key="todo.id">{{todo.item}}</li>
      </transition-group>
    </div>
    <div v-else>Yeah, nothing left todo!</div>
  </transition>
</template>

<script>
// #9
import { ref } from 'vue'

export default {
  emits: ["noValue"],
  setup(props, { emit }) {

    const todos = ref([
      { id: 1, item: 'call mom' },
      { id: 2, item: 'buy food' },
    ])

    const todosLS = JSON.parse(localStorage.getItem('todos'))
    if(todosLS.length) todos.value = todosLS

    const newTodo = ref('')

    const addTodo = () => {
      if(!newTodo.value) {
        emit('noValue')
      } else {
        const id = Math.random();
        todos.value = [{ id, item: newTodo.value }, ...todos.value]
        localStorage.setItem('todos', JSON.stringify(todos.value));
      }

      newTodo.value = ''
    }

    const deleteTodo = (id) => {
      todos.value = todos.value.filter(todo => todo.id !== id)
      localStorage.setItem('todos', JSON.stringify(todos.value));
    }

    return { todos, newTodo, addTodo, deleteTodo };
  }
}
</script>

<style scoped>
  input {
    width: 320px;
    padding: 10px 0;
    border: none;
    border-bottom: 1px solid black;
    margin-bottom: 25px;
  }
  input:focus {
    outline: none;
  }
  ul {
    position: relative;
    width: 320px;
    margin: auto;
    padding: 0;
    color: white;
  }
  li {
    list-style-type: none;
    margin-bottom: 3px;
    padding: 10px;
    background: salmon;
    cursor: pointer;
    width: 100%;
  }

  .list-enter-from { opacity: 0; transform: scale(0.6); }
  .list-enter-to { opacity: 1; transform: scale(1); }
  .list-enter-active { transition: all 0.4s ease; }

  .list-leave-from { opacity: 1; transform: scale(1); }
  .list-leave-to { opacity: 0; transform: scale(0.6); }
  .list-leave-active { transition: all 0.4s ease; position: absolute; }

  .list-move {
    transition: all 0.3 ease;
  }

  .switch-enter-from,
  .switch-leave-to {
    opacity: 0;
    transform: translateY(20px);
  }

  .switch-enter-to,
  .switch-leave-from {
    opacity: 1;
    transform: translateY(0);
  }

  .switch-enter-active,
  .switch-leave-active {
    transition: all 0.5s ease;
  }
</style>

