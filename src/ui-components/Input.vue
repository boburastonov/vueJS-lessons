<template>
  <input
    class="form-control"
    @input="updateInput"
    :value="modelValue"
    type="text"
  />
</template>

<script>
export default {
  name: "Input",
  props: {
    modelValue: {
      type: [String, Number],
      required: true,
    },
  },
  methods: {
    updateInput(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>

<style scoped></style>
