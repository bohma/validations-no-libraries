<template>
  <input
    :value="value"
    :placeholder="placeholder"
    @input="$emit('input', $event.target.value)"
    @blur="$emit('blur', $event.target.value)"
  />
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: "",
    },
    type: {
      type: String,
      default: "name",
    },
    placeholder: {
      type: String,
      default: "Continue",
    },
  },
};
</script>

<style lang="scss" scoped>
input {
  font-family: "Roboto", sans-serif;
  width: 100%;
  padding: 8px 10px;
  margin: 8px 0;
  box-sizing: border-box;
  border-radius: 4px;
  border: solid #e5e5e5 1px;
}
textarea:focus,
input:focus {
  outline: none;
}
</style>
