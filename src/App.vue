<script setup>
import { computed, ref } from "vue";
import CitySelect from "./components/CitySelect.vue";
import Stat from "./components/Stat.vue";
import Error from "./components/Error.vue";

const API_ENDPOINT = "https://api.weatherapi.com/v1";
const errorMap = new Map([[1006, "Указанный город не найден"]]);

let data = ref();
let error = ref();

const errorDisplay = computed(() => {
  return errorMap.get(error.value?.error?.code);
});

const dataModified = computed(() => {
  if (!data.value) {
    return [];
  }

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
    days: 3,
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
    <Error :error="errorDisplay" />
    <Stat v-for="item in dataModified" v-bind="item" :key="item.label" />
    <CitySelect @select-city="getCity" />
  </main>
</template>

<style scoped>
.main {
  background-color: var(--color-bg-main);
  padding: 60px 50px;
  border-radius: 25px;
}
</style>
