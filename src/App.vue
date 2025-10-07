<script setup>
import { computed, ref } from "vue";
import CitySelect from "./components/CitySelect.vue";
import Stat from "./components/Stat.vue";
import Error from "./components/Error.vue";
import DayCard from "./components/DayCard.vue";

const API_ENDPOINT = "https://api.weatherapi.com/v1";
const errorMap = new Map([[1006, "Указанный город не найден"]]);

let data = ref();
let error = ref();
let activeIndex = ref(0);

const errorDisplay = computed(() => {
  return errorMap.get(error.value?.error?.code);
});

const dataModified = computed(() => {
  return [
    {
      label: "Влажность",
      stat: data.value.current.humidity + "%",
    },
    {
      label: "Облачность",
      stat: data.value.current.cloud + "%",
    },
    {
      label: "Ветер",
      stat: data.value.current.wind_kph + " км/ч",
    },
  ];
});

async function getCity(city) {
  const params = new URLSearchParams({
    q: city,
    lang: "ru",
    key: "a8ab481e6f044e13963192750250610",
    days: 4,
  });

  const response = await fetch(
    `${API_ENDPOINT}/forecast.json?${params.toString()}`,
  );

  if (response.status != 200) {
    error.value = await response.json();
    data.value = null;
    return;
  } else {
    error.value = null;
    data.value = await response.json();
  }
}
</script>

<template>
  <main class="main">
    <div class="left-panel"></div>
    <div class="right-panel">
      <Error :error="errorDisplay" />
      <div class="stat-data">
        <div v-if="data">
          <div class="stat-list">
            <Stat
              v-for="item in dataModified"
              v-bind="item"
              :key="item.label"
            />
          </div>
          <div class="day-card-list">
            <DayCard
              v-for="(item, index) in data.forecast.forecastday"
              :key="item.date"
              :is-active="activeIndex === index"
              :weather-code="item.day.condition.code"
              :temperature="item.day.avgtemp_c"
              :date="new Date(item.date)"
              @click="
                () => {
                  activeIndex = index;
                }
              "
            />
          </div>
        </div>
        <CitySelect @select-city="getCity" />
      </div>
    </div>
  </main>
</template>

<style scoped>
.main {
  display: flex;
  align-items: center;
}

.left-panel {
  width: 500px;
  height: 700px;
  border-radius: 30px;
  background: url("./assets/images/background.jpg") no-repeat -299px -267px;
}

.right-panel {
  background-color: var(--color-bg-main);
  padding: 60px 50px;
  border-radius: 25px;
  max-height: 650px;
}

.stat-data {
  display: flex;
  flex-direction: column;
  row-gap: 80px;
}

.stat-list {
  display: flex;
  flex-direction: column;
  row-gap: 16px;
  margin-bottom: 50px;
}

.day-card-list {
  display: flex;
  column-gap: 2px;
}
</style>
