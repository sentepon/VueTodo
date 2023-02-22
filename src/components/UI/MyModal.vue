<template>
  <div class="modal" v-if="show" @click="hideModal">
    <div @click.stop.prevent class="modal__content">
      <slot></slot>
    </div>
  </div>
</template>
<script>
export default {
  name: "MyModal",
  props: {
    show: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    hideModal() {
      this.$emit("update:show", false);
    },
  },
};
</script>
<style scoped>
.modal {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal__content {
  background-color: #fff;
  padding: 1rem 2rem;
}
</style>
