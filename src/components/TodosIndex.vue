<script>
export default {
  props: {
    todos: Array,
  },
};
</script>

<template>
  <div>
    <h1>All Tasks</h1>
    <div v-for="todo in todos" v-bind:key="todo.id">
      <h2>{{ todo.title }}</h2>
      <p>{{ todo.description }}</p>
      <p>
        <label>
          <input type="checkbox" :checked="todo.completed" disabled />
          Completed
        </label>
      </p>
      <button v-on:click="$emit('showTodo', todo)">More info</button>
    </div>
  </div>
</template>

<style></style>
