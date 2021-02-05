<template>
  <div id="weather-info">
    <h1 class="title">
      Taiwan Weather
    </h1>
    <div class="content">
      <template v-if="!filterName">
        <p>Hover</p>
        <p>&</p>
        <p>Click on</p>
      </template>
      <template v-else>
        <p class="content-title">{{ filterName }}</p>
        <div class="contentItem">
          <transition name="fade">
            <template v-if="filterName === currentWheather.locationName">
              <div class="info-list">
                <p>
                  {{ currentWheather.maxT }} ℃ - {{ currentWheather.minT }} ℃
                </p>
                <p>{{ currentWheather.description }}</p>
                <p>{{ currentWheather.comfort }}</p>
                <p>降雨機率: {{ currentWheather.rainPossibility }} %</p>
              </div>
            </template>
          </transition>
        </div>
      </template>
    </div>
    <h1 class="footer">{{ nowDate }}</h1>
  </div>
</template>

<script>
export default {
  name: "WeatherInfo",
  props: {
    filterName: {
      type: String,
      required: true,
    },
    nowDate: {
      type: String,
      required: true,
    },
    currentWheather: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped lang="scss">
@import "../assets/scss/main.scss";

#weather-info {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
  padding: 10px;
  width: 80vh;
  color: $textColor;
  .title {
    position: absolute;
    top: 8%;
    font-size: 60px;
    color: $titleColor;
    text-shadow: 3px 3px 12px gold;
  }
  .content {
    font-size: 50px;
    color: $contentColor;
    text-shadow: 2px 2px 10px gold;
    opacity: 1;
    animation-name: fadeInOpacity;
    animation-iteration-count: 1;
    animation-timing-function: ease-in;
    animation-duration: 2s;
    @keyframes fadeInOpacity {
      0% {
        opacity: 0;
      }
      100% {
        opacity: 1;
      }
    }
    .content-title {
      position: absolute;
      top: 32.5%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }
  .contentItem {
    .fade-enter-active,
    .fade-leave-active {
      transition: opacity 1s;
    }
    .fade-enter,
    .fade-leave-to {
      opacity: 0;
    }
    .info-list {
      padding: 10px;
      margin-top: 20px;
      text-align: center;
      font-size: 20px;
      font-weight: normal;
      color: $contentColor;
      text-shadow: 1px 1px 5px gold;
      border: 1px solid #fff;
      p {
        margin: 5px;
      }
    }
  }
  .footer {
    position: absolute;
    bottom: 10%;
    font-size: 20px;
    font-weight: normal;
    color: $contentColor;
    text-shadow: 2px 2px 10px gold;
  }
}
</style>
