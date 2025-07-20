<script>
import axios from "axios";
import TodosIndex from "./TodosIndex.vue";

export default {
  name: "Content",
  components: {
    TodosIndex,
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
  },
};
</script>

<template>
  <main>
    <TodosIndex v-bind:todos="todos" />
  </main>
</template>

<style></style>
