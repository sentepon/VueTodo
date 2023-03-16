<template>
  <li class="todo-list__item">
    <label class="todo-list__label">
      <input
        type="checkbox"
        class="todo-list__input"
        :checked="todo.completed"
        @change="changeCompleted"
      />
      <p class="todo-list__title">
        {{ todo.title }}
      </p>
    </label>
    <time class="todo-list__time">
      {{ todo.time }}
    </time>
  </li>
</template>
<script>
export default {
  props: {
    todo: {
      type: Object,
    },
  },
  methods: {
    changeCompleted(event) {
      this.$emit("changeCompleted", event.target.checked, this.todo);
    },
  },
};
</script>
<style>
.todo-list__item {
  list-style-type: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
}
.todo-list__label {
  display: flex;
  gap: 0.2rem;
  align-items: center;
}
</style>
