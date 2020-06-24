<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import AddTodo from "./components/AddTodo.vue";
import Header from "./components/layout/header.vue";
import Todos from "./components/Todos.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    Todos,
    Header,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(res => (this.todos = res.data))
      .catch(err => console.log(err));
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => this.todos = this.todos.filter(todos =>todos.id !== id, res.data))
      .catch(err => console.log(err))
    },
    addTodo(newTodo) {
      const {title, completed} = newTodo
      axios.post("https://jsonplaceholder.typicode.com/todos",
      {title,completed})
      .then(res => this.todos = [...this.todos, res.data])
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.5;
}
</style>
