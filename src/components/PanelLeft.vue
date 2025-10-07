<script setup>
import { computed, inject } from "vue";
import WeatherIcon from "./WeatherIcon.vue";
import { cityProvide } from "../constants";

const city = inject(cityProvide);
const TEMPERATURE_MEASURE = "℃";

const { dayData } = defineProps({
  dayData: Object,
});

const temperature = computed(() => {
  {
    return dayData.day.avgtemp_c + TEMPERATURE_MEASURE;
  }
});

const currentDate = computed(() => {
  return new Date(dayData.date);
});

const weatherCode = computed(() => {
  return dayData.day.condition.code;
});
</script>

<template>
  <div v-if="dayData" class="panel-left">
    <div class="panel panel-left__top">
      <WeatherIcon :weather-code />
      <span class="temperature">
        {{ temperature }}
      </span>
      <div class="panel-left__day">
        {{
          currentDate.toLocaleDateString("ru-RU", {
            weekday: "long",
          })
        }}
      </div>
    </div>

    <div class="panel panel-left__bottom">
      <div class="panel-left__date">
        {{
          currentDate.toLocaleDateString("ru-RU", {
            day: "numeric",
            month: "long",
            year: "numeric",
          })
        }}
      </div>
      <div class="city">
        {{ city }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.panel-left {
  width: 500px;
  height: 700px;
  color: var(--color-primary-inverted);
  font-size: 25px;
  display: flex;
  flex-direction: column;
  border-radius: 30px;
  background: url("../assets/images/background.jpg") no-repeat -299px -267px;
}

.panel {
  --margin: 50px;
  margin-left: var(--margin);
}

.panel-left__top {
  margin-top: var(--margin);
  /* margin-bottom: var(--margin); */
}

.panel-left__day::first-letter {
  text-transform: uppercase;
}

.temperature {
  font-size: 40px;
  margin-left: 20px;
}
</style>
