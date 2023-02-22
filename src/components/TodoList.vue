<template>
  <ul class="todo-list" :key="todo.id" v-for="todo in todos">
    <li class="todo-list__item">
      <label class="todo-list__label">
        <input
          type="checkbox"
          class="todo-list__input"
          :checked="todo.completed"
        />
        <p class="todo-list__title">
          {{ todo.title }}
        </p>
        <time class="todo-list__time">
          {{ todo.time }}
        </time>
      </label>
    </li>
  </ul>
</template>
<script>
export default {
  props: {
    todos: {
      type: Array,
    },
  },
};
</script>
<style>
.todo-list__item {
  list-style-type: none;
}
.todo-list__label {
  display: flex;
  justify-content: flex-start;
}
.todo-list__time {
  justify-self: end;
}
</style>
