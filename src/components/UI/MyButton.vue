<template>
  <button>
    <slot></slot>
  </button>
</template>
<script>
export default {
  name: "MyButton",
};
</script>
<style scoped>
button {
  font-family: "Montserrat";
  font-size: 18px;
  background-color: transparent;
  padding: 5px 10px;
  border: 1px solid black;
  border-radius: 3px;
  height: 2rem;
}
</style>
