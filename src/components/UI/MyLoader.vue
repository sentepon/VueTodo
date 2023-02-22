<template>
  <div class="loader"></div>
</template>
<script>
export default {
  name: "MyLoader",
};
</script>
<style scoped>
.loader {
  width: 4rem;
  height: 4rem;
  border: 0.5rem solid grey;
  border-radius: 50%;
  border-top-color: transparent;
  animation-name: loader;
  animation-duration: 1s;
  animation-iteration-count: infinite;
}
@keyframes loader {
  0% {
    visibility: visible;
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
