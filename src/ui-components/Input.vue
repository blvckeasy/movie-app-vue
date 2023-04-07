<template>
  <input type="text" class="form-control" :value="modelValue" @input="updateInput">
</template>

<script>
export default {
  name: "Input",
  props: {
    modelValue: [String, Number],
  },
  methods: {
    updateInput(event) {
      this.$emit("update:modelValue", event.target.value)
    }
  }
}
</script>

<style></style>
