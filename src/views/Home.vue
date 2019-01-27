<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:data="todo_list" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import axios from "axios";

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todo_list: []
    }
  },
  methods:{
    deleteTodo(id){
      // Call API to delete
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => this.todo_list = this.todo_list.filter(todo => todo.id !== id))
        .catch(err => console.log(err))
    },
    addTodo(newTodo){
      // Add new task to API
      const { title, completed } = newTodo

      axios.post("https://jsonplaceholder.typicode.com/todos",{
        title,
        completed
      })
        .then(res => this.todo_list = [...this.todo_list, res.data])
        .catch(err => console.log(err))
    }
  },
  created() {
    axios.get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(res => this.todo_list = res.data)
      .catch(err => console.log(err))
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
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>
