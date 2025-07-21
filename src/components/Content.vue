<script>
import axios from "axios";
import TodosIndex from "./TodosIndex.vue";
import TodosNew from "./TodosNew.vue";

export default {
  name: "Content",
  components: {
    TodosIndex,
    TodosNew,
  },
  data: function () {
    return {
      todos: [
        // { title: "Todo 1", description: "This is todo 1", completed: false },
        // { title: "Todo 2", description: "This is todo 2", completed: true },
        // { title: "Todo 3", description: "This is todo 3", completed: false },
      ],
    };
  },
  created: function () {
    this.handleIndexTodos();
  },
  methods: {
    handleIndexTodos: function () {
      axios.get("/todos.json").then((response) => {
        console.log("todos index", response);
        this.todos = response.data;
      });
    },
    handleCreateTodo: function (params) {
      axios
        .post("/todos.json", params)
        .then((response) => {
          console.log("todos create", response);
          this.todos.push(response.data);
        })
        .catch((error) => {
          console.log("todos create error", error.response);
        });
    },
  },
};
</script>

<template>
  <main>
    <TodosNew v-on:createTodo="handleCreateTodo" />
    <TodosIndex v-bind:todos="todos" />
  </main>
</template>

<style></style>
