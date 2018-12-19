<template>
  <div>
    <input
      type="text"
      class="todo-input"
      placeholder="What needs to be done"
      v-model="newTodo"
      @keyup.enter="addTodo"
    >
    <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
      <div class="todo-item-left">
        <div 
          class="todo-item-label"
          v-if="!todo.editing"
          @dblclick="editTodo(todo)"
        >
          {{todo.task}}
        </div>
        <input
          class="todo-item-edit"
          type="text" 
          v-model="todo.task"
          v-else
          v-focus
          @blur="doneEdit(todo)"
          @keyup.enter="doneEdit(todo)"
          @keyup.escape="cancelEdit(todo)"
        >
      </div>
      <div 
        class="remove-item"
        @click="removeTodo(index)"
      >
        &times;
      </div>
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
      beforeEditCache: '',
      todos: [
        {
          id: 1,
          task: 'Eat lunch',
          completed: false,
          editing: false
        },
        {
          id: 2,
          task: 'Learn code',
          completed: false,
          editing: false
        }
      ]
    }
  },
  directives: {
    focus: {
      inserted: function (el) {
        el.focus()
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length === 0) {
        return
      }
      this.todos.push({
        id: this.idForTodo,
        task: this.newTodo,
        completed: false
      })
      this.newTodo = ''
      this.idForTodo++
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
    },
    editTodo(todo) {
      this.beforeEditCache = todo.task
      todo.editing = true
    },
    doneEdit(todo) {
      if (todo.task.trim().length === 0) {
        todo.task = this.beforeEditCache
      }
      todo.editing = false
    },
    cancelEdit(todo) {
      todo.task = this.beforeEditCache
      todo.editing = false
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

  .todo-item {
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .remove-item {
    cursor: pointer;
    margin-left: 14px;
    &:hvoer {
      color: black;
    }
  }

  .todo-item-left {
    display: flex;
    align-items: center;
  }

  .todo-item-label {
    padding: 10px;
    border: 1px solid white;
    margin-left: 12px;
  }

  .todo-item-edit {
    font-size: 24px;
    color: #2c3e50;
    margin-left: 12px;
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc; //override defaults
    font-family: "Avenir", Helvetica, Arial, sans-serif;

    &:focus {
      outline: none;
    }
  }
</style>
