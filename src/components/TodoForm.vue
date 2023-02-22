<template>
  <form class="form" @submit.prevent>
    <label class="form__label">
      <input
        type="text"
        class="form__task"
        placeholder="Введите задачу"
        v-model="todo.title"
      />
      <input type="time" class="form__time" v-model="todo.time" />
      <button class="form__btn" @click="addTodo">Добавить задачу</button>
    </label>
  </form>
</template>
<script>
export default {
  data() {
    return {
      todo: {
        title: "",
        time: "",
        id: "",
      },
    };
  },
  methods: {
    addTodo() {
      this.todo.id = Date.now();
      this.$emit("addTodo", this.todo);
      this.todo = {
        title: "",
        time: "",
        id: "",
      };
    },
  },
};
</script>
<style></style>
