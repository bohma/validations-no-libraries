<template>
  <button
    @click="click"
    class="btn"
    :style="{
      border: border,
      color: color,
      width: width,
      height: height,
      padding: padding,
      fontSize: fontSize,
      background: background,
    }"
  >
    <slot>{{ title }}</slot>
  </button>
</template>

<script>
export default {
  name: "v-btn",
  data() {
    return {};
  },
  props: {
    title: {
      type: String,
      default: "Continue",
    },
    padding: {
      type: String,
      default: "10px",
    },
    width: {
      type: String,
    },
    height: {
      type: String,
    },
    fontSize: {
      type: String,
      default: "14px",
    },
    border: {
      type: String,
      default: "none",
    },
    color: {
      type: String,
      default: "#fff",
    },
    background: {
      type: String,
      default: "#00D395",
    },
  },
  methods: {
    async click() {
      this.$emit("click");
    },
  },
};
</script>

<style lang="scss" scoped>
.btn {
  font-family: "Roboto", sans-serif;
  border-radius: 5px;
  cursor: pointer;
}
</style>
