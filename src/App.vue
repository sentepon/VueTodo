<template>
  <div class="container app">
    <div class="menu">
      <ul class="menu__list">
        <li class="menu__item" :key="nextDates[day]" v-for="day in nextDates">
          <a href="" class="menu__link">{{
            day.toLocaleString("ru", this.options)
          }}</a>
        </li>
      </ul>
    </div>
    <div class="todo">
      <h2>Список задач</h2>
      <todo-form @addTodo="addTodo"></todo-form>
      <todo-list :todos="todos" v-if="!isTodosLoading"></todo-list>
      <my-loader v-else></my-loader>
    </div>
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
      currentDate: new Date(),
      numberOfNextDays: 5,
      nextDates: [],
      options: {
        month: "long",
        day: "numeric",
      },
    };
  },
  methods: {
    addTodo(todo) {
      this.todos.unshift(todo);
    },
    getNextDate(data) {
      let tomorrow = new Date();
      tomorrow.setDate(data.getDate() + 1);
      return tomorrow;
    },
    getNextDates(date) {
      for (let i = 0; i < this.numberOfNextDays; i++) {
        this.nextDates.push(date);
        date = this.getNextDate(date);
      }
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
    this.getNextDates(this.currentDate);
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
.app {
  display: grid;
  grid-template-columns: 8rem 1fr;
}
</style>
