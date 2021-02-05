<template>
  <div class="spinner-wrap">
    <div class="spinner-content">
      <div class="spinner-item">
        <img src="@/assets/images/sun.svg" alt="sun" />
        <img src="@/assets/images/cloudy.svg" alt="cloudy" />
        <img src="@/assets/images/snow.svg" alt="snow" />
      </div>
      <p class="spinner-title" @click="handleClick">Enter</p>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    handleClick() {
      this.$emit("loadingHandler");
    },
  },
};
</script>

<style scoped lang="scss">
@import "../assets/scss/main.scss";
@import url("https://fonts.googleapis.com/css2?family=Kumar+One+Outline&display=swap");

img {
  height: 10vh;
}
.spinner-wrap {
  font-family: "Kumar One Outline", cursive;
  position: absolute;
  top: 0px;
  left: 0px;
  height: 100%;
  width: 100%;
  background-color: $loadingColor;
  .spinner-content {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    .spinner-title {
      color: #fff;
      letter-spacing: 2px;
      font-size: 30px;
      cursor: pointer;
      text-shadow: 0 0 5px rgba(255, 65, 65, 1), 0 0 10px rgba(255, 65, 65, 1),
        0 0 20px rgba(255, 65, 65, 1), 0 0 40px rgba(255, 65, 65, 1);
      animation: title-shine 2s 1s linear infinite;
    }
    .spinner-item {
      margin: 10px;
      img {
        margin: 10px;
      }
    }
    .spinner-item > img {
      animation: spinner-item 0.9s infinite alternate;
    }
    .spinner-item > img:nth-child(2) {
      animation-delay: 0.5s;
    }
    .spinner-item > img:nth-child(3) {
      animation-delay: 0.7s;
    }
    @keyframes spinner-item {
      from {
        opacity: 1;
        /* transform: translateY(0rem); */
        transform: rotateY(-180deg);
      }
      to {
        opacity: 0.1;
        transform: translateY(-3rem);
      }
    }
    @keyframes title-shine {
      0% {
        opacity: 1;
      }
      90% {
        opacity: 0;
      }
      100% {
        color: #fff;
      }
    }
  }
}
</style>
