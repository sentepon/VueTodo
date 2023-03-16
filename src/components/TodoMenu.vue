<template>
  <div class="menu">
    <h1>ToDo</h1>
    <ul class="menu__list">
      <li
        class="menu__item"
        :key="dates[date]"
        v-for="date in dates"
        @click="changeSelectedDate(date)"
      >
        <a href="#" class="menu__link">{{
          date.toLocaleString("ru", this.options)
        }}</a>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props: {
    dates: {
      type: Array,
    },
    modelValue: {
      type: Object,
    },
    options: {
      type: Object,
    },
  },
  methods: {
    changeSelectedDate(date) {
      this.$emit("update:modelValue", date);
    },
  },
};
</script>
<style>
.menu__item {
  list-style-type: none;
}
.menu__link {
  color: #000;
  text-decoration: none;
}
</style>
