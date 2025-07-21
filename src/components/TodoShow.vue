<script>
export default {
  props: {
    todo: Object,
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
  </div>
</template>

<style></style>
