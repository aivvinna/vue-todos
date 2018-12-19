<template>
  <div class="home container">
    <img alt="Vue logo" src="../assets/logo.png" class="logo">
    <TodoList></TodoList>
  </div>
</template>

<script>
// @ is an alias to /src
import TodoList from '@/components/TodoList.vue'

export default {
  name: 'home',
  components: {
    TodoList
  }
}
</script>

<style>
.container {
  max-width: 600px;
  margin: 0 auto;
}

.logo {
  display: block;
  margin: 20px auto;
  height: 75px;
}
</style>
