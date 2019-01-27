<template>
  <div id="app">
    <Todos v-bind:data="todo_list" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from "./components/Todos";

export default {
  name: 'app',
  components: {
    Todos
  },
  data() {
    return {
      todo_list: [
        {
          id: 1,
          title: 'Task 1',
          completed: false,
        },
        {
          id: 2,
          title: 'Task 2',
          completed: true,
        },
        {
          id: 3,
          title: 'Task 3',
          completed: false,
        }
      ]
    }
  },
  methods:{
    deleteTodo(id){
      this.todo_list = this.todo_list.filter(todo => todo.id !== id)
    }
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
</style>
