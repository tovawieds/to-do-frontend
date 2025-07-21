<script>
export default {
  props: {
    todo: Object,
  },
  data: function () {
    return {
      editTodoParams: {},
    };
  },
  created: function () {
    this.editTodoParams = {
      ...this.todo,
      completed: this.todo.completed === true || this.todo.completed === "true" || this.todo.completed === 1,
    };
  },
  methods: {
    handleSubmit: function () {
      this.$emit("updateTodo", this.todo.id, this.editTodoParams);
    },
  },
};
</script>

<template>
  <div>
    <h1>Task information</h1>
    <p>Title: {{ todo.title }}</p>
    <p>Description: {{ todo.description }}</p>
    <p>
      <label>
        <input type="checkbox" :checked="todo.completed" disabled />
        Completed
      </label>
    </p>
    <form v-on:submit.prevent="handleSubmit">
      <div>
        Title:
        <input v-model="editTodoParams.title" type="text" />
      </div>
      <div>
        Description:
        <input v-model="editTodoParams.description" type="text" />
      </div>
      <div>
        Completed:
        <input v-model="editTodoParams.completed" type="checkbox" />
      </div>
      <button type="submit">Update Task</button>
    </form>
    <button v-on:click="$emit('destroyTodo', todo)">Delete Task</button>
  </div>
</template>

<style></style>
