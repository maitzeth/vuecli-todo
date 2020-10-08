<template>
  <div id="app">
    <AddForm v-on:add-todo="handleAddTodo" />
    <Todos :todos="todos" v-on:del-todo="handleDeleteTodo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddForm from "../components/AddForm";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Todos,
    AddForm,
  },
  data() {
    return {
      todos: [],
    };
  },
  created() {
    this.getTodos();
  },
  methods: {
    async handleDeleteTodo(id) {
      await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);

      this.todos = this.todos.filter((item) => item.id !== id);
    },
    async handleAddTodo(newTodo) {
      const { title, completed } = newTodo;

      const response = await axios.post(
        "https://jsonplaceholder.typicode.com/todos",
        {
          title,
          completed,
        }
      );

      this.todos = [...this.todos, response.data];
    },
    async getTodos() {
      const response = await axios.get(
        "https://jsonplaceholder.typicode.com/todos?_limit=5"
      );

      this.todos = response.data;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: sans-serif;
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
