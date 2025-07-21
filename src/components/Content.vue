<script>
import axios from "axios";
import TodosIndex from "./TodosIndex.vue";
import TodosNew from "./TodosNew.vue";
import TodoShow from "./TodoShow.vue";
import Modal from "./Modal.vue";

export default {
  name: "Content",
  components: {
    TodosIndex,
    TodosNew,
    TodoShow,
    Modal,
  },
  data: function () {
    return {
      todos: [
        // { title: "Todo 1", description: "This is todo 1", completed: false },
        // { title: "Todo 2", description: "This is todo 2", completed: true },
        // { title: "Todo 3", description: "This is todo 3", completed: false },
      ],
      currentTodo: {},
      isTodoShowVisible: false,
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
    handleShowTodo: function (todo) {
      console.log("handleShowTodo", todo);
      this.currentTodo = todo;
      this.isTodoShowVisible = true;
    },
    handleUpdateTodo: function (id, params) {
      console.log("handleUpdateTodo", id, params);
      axios
        .patch(`/todos/${id}.json`, params)
        .then((response) => {
          console.log("todos update", response);
          this.todos = this.todos.map((todo) => {
            if (todo.id === id) {
              return response.data;
            } else {
              return todo;
            }
          });
          this.handleClose();
        })
        .catch((error) => {
          console.log("todos update error", error.response);
        });
    },
    handleDestroyTodo: function (todo) {
      axios.delete(`/todos/${todo.id}.json`).then((response) => {
        console.log("todo destroy", response);
        var index = this.todos.indexOf(todo);
        this.todos.splice(index, 1);
        this.handleClose();
      });
    },
    handleClose: function () {
      this.isTodoShowVisible = false;
    },
  },
};
</script>

<template>
  <main>
    <TodosNew v-on:createTodo="handleCreateTodo" />
    <TodosIndex v-bind:todos="todos" v-on:showTodo="handleShowTodo" />
    <Modal v-bind:show="isTodoShowVisible" v-on:close="handleClose">
      <TodoShow v-bind:todo="currentTodo" v-on:updateTodo="handleUpdateTodo" v-on:destroyTodo="handleDestroyTodo" />
    </Modal>
  </main>
</template>

<style></style>
