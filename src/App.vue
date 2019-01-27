<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:data="todo_list" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";

export default {
  name: 'app',
  components: {
    Header,
    Todos,
    AddTodo
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
    },
    addTodo(newTodo){
      this.todo_list = [...this.todo_list,newTodo]
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
