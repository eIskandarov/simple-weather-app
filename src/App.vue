<script setup>
import { onMounted, provide, ref, watch } from "vue";
import PanelRight from "./components/PanelRight.vue";
import PanelLeft from "./components/PanelLeft.vue";
import { API_ENDPOINT, cityProvide } from "./constants";

let data = ref();
let error = ref();
let activeIndex = ref(0);

let city = ref("Москва");
provide(cityProvide, city);

watch(city, () => {
  getCity(city.value);
});

onMounted(() => {
  getCity(city.value);
});

async function getCity(city) {
  const apiKey = import.meta.env.VITE_API_KEY;
  const params = new URLSearchParams({
    q: city,
    lang: "ru",
    key: `${apiKey}`,
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
    <PanelLeft :day-data="data?.forecast.forecastday[activeIndex]" />
    <PanelRight
      :data
      :error
      :active-index="activeIndex"
      @select-index="(index) => (activeIndex = index)"
    />
  </main>
</template>

<style scoped>
.main {
  display: flex;
  align-items: center;
}
</style>
