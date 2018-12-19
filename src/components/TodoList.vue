<template>
  <div>
    <input
      type="text"
      class="todo-input"
      placeholder="What needs to be done"
      v-model="newTodo"
      @keyup.enter="addTodo"
    >
    <div v-for="todo in todos" :key="todo.id" class="todo-item">
      {{todo.task}}
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      newTodo: '',
      idForTodo: 3,
      todos: [
        {
          id: 1,
          task: 'Eat lunch',
          completed: false
        },
        {
          id: 2,
          task: 'Learn code',
          completed: false
        }
      ]
    }
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.idForTodo,
        task: this.newTodo,
        completed: false
      })

      this.newTodo = ''
      this.idForTodo++
    }
  }
}
</script>

<style lang="scss">
  .todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 16px;

    &:focus {
      outline: 0;
    }
  }
</style>
