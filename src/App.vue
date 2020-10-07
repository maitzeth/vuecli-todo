<template>
  <div id="app">
    <Header />
    <AddForm v-on:add-todo="handleAddTodo" />
    <Todos :todos="todos" v-on:del-todo="handleDeleteTodo" />
  </div>
</template>

<script>
import Header from "./components/Layout/Header";
import Todos from "./components/Todos";
import AddForm from "./components/AddForm";

export default {
  name: "App",
  components: {
    Header,
    Todos,
    AddForm,
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Todo one",
          completed: false,
        },
        {
          id: 2,
          title: "Todo two",
          completed: false,
        },
        {
          id: 3,
          title: "Todo three",
          completed: false,
        },
      ],
    };
  },
  methods: {
    handleDeleteTodo(id) {
      this.todos = this.todos.filter((item) => item.id !== id);
    },
    handleAddTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
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
