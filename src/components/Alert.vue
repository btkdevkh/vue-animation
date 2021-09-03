<template>
  <div class="alert">{{msg}}</div>
</template>

<script>
export default {
  props: ['msg']
}
</script>

<style scope>
  .alert {
    position: absolute;
    top: 15px;
    left: 10px;
    right: 10px;
    width: 300px;
    margin: 0 auto;
    padding: 10px 0;
    color: white;
    background: orange;
  }
</style>