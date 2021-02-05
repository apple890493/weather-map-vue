<template>
  <div id="app">
    <template v-if="isLoading">
      <!-- <div> -->
      <Spinner @loadingHandler="loadingHandler" />
      <!-- </div> -->
    </template>
    <template v-else>
      <TaiwanMap
        @catchFilterValue="catchFilterValue"
        @catchCityValue="catchCityValue"
      />
      <WeatherInfo
        :filterName="filterName"
        :nowDate="nowDate"
        :currentWheather="currentWheather"
      />
    </template>
  </div>
</template>

<script>
import TaiwanMap from "./components/TaiwanMap.vue";
import WeatherInfo from "./components/WeatherInfo.vue";
import Spinner from "./components/Spinner.vue";
import { parseDate2Str } from "@/util/helper.js";
import axios from "axios";

const AUTHORIZATION_KEY = "CWB-3808BCC0-8B91-4A9F-99FC-D105A91BCAB1";

export default {
  name: "App",
  components: {
    TaiwanMap,
    WeatherInfo,
    Spinner,
  },
  data() {
    return {
      filterName: "",
      nowDate: parseDate2Str(new Date(), "YYYY-MM-DD HH:mm:ss"),
      timer: "",
      isLoading: true,
      currentWheather: {
        locationName: "",
        description: "",
        comfort: "",
        maxT: 0,
        mixT: 0,
        rainPossibility: 0,
      },
    };
  },
  methods: {
    loadingHandler() {
      this.isLoading = !this.isLoading;
    },
    catchFilterValue: function(val) {
      if (!val) {
        return;
      }
      this.filterName = val;
    },
    catchCityValue: function(val) {
      if (!val) {
        return;
      }
      this.getCurrentWeather(val);
    },
    getCurrentWeather(LOCATION_NAME) {
      axios
        .get(
          `https://opendata.cwb.gov.tw/api/v1/rest/datastore/F-C0032-001?Authorization=${AUTHORIZATION_KEY}&locationName=${LOCATION_NAME}`
        )
        .then((res) => {
          const locationName = res.data.records.location[0].locationName;
          const records = res.data.records.location[0].weatherElement;
          const wx = records[0].time[0].parameter.parameterName;
          const pop = records[1].time[0].parameter.parameterName;
          const minT = records[2].time[0].parameter.parameterName;
          const ci = records[3].time[0].parameter.parameterName;
          const maxT = records[4].time[0].parameter.parameterName;

          console.log(res);
          this.currentWheather = {
            locationName,
            description: wx,
            comfort: ci,
            rainPossibility: pop,
            minT,
            maxT,
          };
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  created() {
    this.timer = setInterval(() => {
      this.nowDate = parseDate2Str(new Date(), "YYYY-MM-DD HH:mm:ss");
    }, 1000);
  },
  beforeDestroy() {
    if (this.timer) {
      clearInterval(this.timer);
    }
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Lobster&display=swap");
@import "./assets/scss/main.scss";
@import "./assets/rest.css";

#app {
  font-family: Lobster, cursive, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: $nightBgColor;
  display: flex;
  justify-content: center;
}
</style>
