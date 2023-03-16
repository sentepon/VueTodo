<template>
  <form class="form" @submit.prevent>
    <label class="form__label">
      <my-input
        type="text"
        class="form__task"
        placeholder="Введите задачу"
        v-model="todo.title"
      />
      <my-input type="time" class="form__time" v-model="todo.time" />
      <my-button class="form__btn" @click="addTodo">Добавить задачу</my-button>
    </label>
  </form>
</template>
<script>
export default {
  props: {
    currentDate: {},
  },
  data() {
    return {
      todo: {
        id: "",
        title: "",
        time: "",
        completed: "",
      },
    };
  },
  methods: {
    addTodo() {
      this.todo.id = Date.now();
      this.todo.completed = false;
      this.$emit("addTodo", this.todo);
      this.todo = {
        id: "",
        title: "",
        time: "",
        completed: "",
      };
    },
  },
};
</script>
<style></style>
