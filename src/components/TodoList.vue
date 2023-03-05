<template>
  <ul class="todo-list">
    <todo-item
      class="todo-list__item"
      :key="todo.id"
      v-for="todo in todos"
      :todo="todo"
      @changeCompleted="changeCompleted"
    >
    </todo-item>
  </ul>
</template>
<script>
import TodoItem from "./TodoItem.vue";
export default {
  components: { TodoItem },
  props: {
    todos: {
      type: Array,
    },
  },
  methods: {
    changeCompleted(checked, todo) {
      this.$emit("changeCompleted", checked, todo);
    },
  },
};
</script>
<style></style>
