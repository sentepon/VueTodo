<template>
  <input @input="update" :value="modelValue" />
</template>
<script>
export default {
  name: "MyInput",
  props: {
    modelValue: {
      type: [String, Number],
      required: true,
    },
  },
  methods: {
    update(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>
<style>
input {
  font-family: "Montserrat";
  font-size: 18px;
  padding: 5px 10px;
  border: 1px solid black;
  border-radius: 3px;
  height: 2rem;
}
</style>
