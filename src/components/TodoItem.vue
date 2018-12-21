<template>
  <div class="todo-item">
    <div class="todo-item-left">
      <input type="checkbox" v-model="completed">
      <div 
        class="todo-item-label"
        :class="{completed: completed}"
        v-if="!editing"
        @dblclick="editTodo">
        {{task}}
      </div>
      <input
        class="todo-item-edit"
        type="text" 
        v-model="task"
        v-else
        v-focus
        @blur="doneEdit"
        @keyup.enter="doneEdit"
        @keyup.escape="cancelEdit">
    </div>
    <div 
      class="remove-item"
      @click="removeTodo(index)">
      &times;
    </div>
  </div>
</template>

<script>
export default {
  name: 'todo-item',
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
    checkAll: {
      type: Boolean,
      required: true,
    }
  },
  data() {
    return {
      id: this.todo.id,
      task: this.todo.task,
      completed: this.todo.completed,
      editing: this.todo.completed,
      beforeEditCache: '',
    }
  },
  watch: {
    checkAll() {
      this.completed = this.checkAll ? true : this.todo.completed
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
    removeTodo(index) {
      this.$emit('removedTodo', index)
    },
    editTodo() {
      this.beforeEditCache = this.task
      this.editing = true
    },
    doneEdit() {
      if (this.task.trim().length === 0) {
        this.task = this.beforeEditCache
      }
      this.editing = false
      this.$emit('finishedEdit', {
        index: this.index,
        todo: {
          id: this.id,
          title: this.title,
          completed: this.completed,
          editing: this.editing
        }
      })
    },
    cancelEdit() {
      this.task = this.beforeEditCache
      this.editing = false
    },
  }
}
</script>
