<template>
  <div id="theme-setting">
    <div class="theme-options">
      <div
        id="theme-light"
        :class="{ active: currentTheme === 'theme-light' }"
        @click="toggleTheme('theme-light')"
      ></div>
      <div
        id="theme-dark"
        :class="{ active: currentTheme === 'theme-dark' }"
        @click="toggleTheme('theme-dark')"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    currentTheme: {
      type: String,
      required: true,
    },
  },
  methods: {
    toggleTheme(theme) {
      this.$emit("swicthTheme", theme);
    },
  },
};
</script>

<style scoped lang="scss">
.theme-options {
  position: absolute;
  top: 5%;
  right: 5%;
  padding: 20px 0;
  div {
    cursor: pointer;
    width: 20px;
    height: 20px;
    border-radius: 4px;
    margin: 2px 10px;
    border: 1px solid #fff;
    display: inline-block;
    opacity: 0.5;
    &:hover {
      opacity: 1;
    }
    &.active {
      opacity: 1;
    }
  }
  #theme-light {
    background-color: #ffe2e2;
  }
  #theme-dark {
    background-color: #112d4e;
  }
}
</style>
