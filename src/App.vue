<template>
  <div class="container app">
    <todo-menu
      :dates="dates"
      :options="options"
      v-model="selectedDate"
    ></todo-menu>
    <div class="todo">
      <h2>Список задач</h2>
      <strong>{{ selectedDate.toLocaleString("ru", options) }}</strong>
      <todo-form
        @addTodo="addTodo"
        :currentDate="currentDate.toLocaleDateString()"
      ></todo-form>
      <todo-list
        :todos="selectedTodos"
        v-if="!isTodosLoading"
        @changeCompleted="changeCompleted"
      ></todo-list>
      <my-loader v-else></my-loader>
      <my-button v-if="isCompletedTodo">Удалить выполненные задачи</my-button>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import TodoList from "./components/TodoList.vue";
import TodoForm from "./components/TodoForm.vue";
import TodoMenu from "./components/TodoMenu.vue";

export default {
  components: {
    TodoList,
    TodoForm,
    TodoMenu,
  },
  data() {
    return {
      todos: [],
      limit: 5,
      isTodosLoading: false,
      show: false,
      currentDate: new Date(),
      numberOfNextDays: 5,
      dates: [],
      selectedDate: {},
      options: {
        month: "long",
        day: "numeric",
      },
      options2: {
        month: "2-digit",
        day: "2-digit",
        year: "numeric",
      },
    };
  },
  methods: {
    addTodo(todo) {
      todo.date = this.selectedDate;
      this.todos.unshift(todo);
    },
    getNextDate(data) {
      let tomorrow = new Date();
      tomorrow.setDate(data.getDate() + 1);
      return tomorrow;
    },
    getDates(date) {
      for (let i = 0; i < this.numberOfNextDays; i++) {
        this.dates.push(date);
        date = this.getNextDate(date);
      }
    },
    changeCompleted(checked, todo) {
      this.todos.forEach((orTodo) => {
        if (todo.id === orTodo.id) {
          orTodo.completed = checked;
        }
      });
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
        this.todos.forEach((todo) => {
          todo.date = this.selectedDate;
          todo.time = "12:30";
        });
      } catch (e) {
        alert("Error");
      } finally {
        this.isTodosLoading = false;
      }
    },
  },
  mounted() {
    this.fetchTodos();
    this.getDates(this.currentDate);
    this.selectedDate = this.currentDate;
  },
  computed: {
    selectedTodos() {
      return this.todos.filter((todo) => todo.date === this.selectedDate);
    },
    isCompletedTodo() {
      let result = false;
      this.selectedTodos.forEach((todo) => {
        if (todo.completed === true) {
          result = true;
        }
      });
      return result;
    },
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
