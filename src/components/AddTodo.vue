<template>
  <div>
    <form @submit="addTodo">
      <input type="text" name="title" placeholder="Add your task..." v-model="title">
      <input type="submit" value="Submit" class="btn">
    </form>
  </div>
</template>

<script>
import uuid from "uuid";

export default {
  name: 'AddTodo',
  data() {
    return {
      title: ''
    }
  },
  methods: {
    addTodo(e) {
      // Don't reload page when submit
      e.preventDefault()

      const newTodo = {
        id: uuid.v4(),
        title: this.title,
        completed: false
      }

      // Send up to parent
      this.$emit('add-todo', newTodo)

      // Clear after submit
      this.title = ''
    }
  }
}
</script>

<style scoped>
  form {
    display: flex;
  }
  input[type="text"] {
    flex: 10;
    padding: 5px;
  }
  input[type="submit"] {
    flex: 2;
  }
</style>
