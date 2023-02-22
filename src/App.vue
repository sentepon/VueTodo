<template>
  <div class="container">
    <h2>Список задач</h2>
    <my-modal v-model:show="show"> </my-modal>
    <todo-form @addTodo="addTodo"></todo-form>
    <todo-list :todos="todos" v-if="!isTodosLoading"></todo-list>
    <my-loader v-else></my-loader>
  </div>
</template>
<script>
import axios from "axios";
import TodoList from "./components/TodoList.vue";
import TodoForm from "./components/TodoForm.vue";

export default {
  components: {
    TodoList,
    TodoForm,
  },
  data() {
    return {
      todos: [],
      limit: 15,
      isTodosLoading: false,
      show: false,
    };
  },
  methods: {
    addTodo(todo) {
      this.todos.unshift(todo);
    },
    async fetchTodos() {
      try {
        this.isTodosLoading = true;
        const res = await axios.get(
          "https://jsonplaceholder.typicode.com/todos",
          {
            params: {
              _limit: this.limit,
            },
          }
        );
        this.todos = res.data;
      } catch (e) {
        alert("Error");
      } finally {
        this.isTodosLoading = false;
      }
    },
  },
  mounted() {
    this.fetchTodos();
  },
};
</script>
<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.container {
  max-width: calc(1440px + 2rem);
  padding-inline: 1rem;
  margin-inline: auto;
}
</style>
