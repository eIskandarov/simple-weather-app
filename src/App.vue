<script setup>
import { ref } from "vue";
import PanelRight from "./components/PanelRight.vue";

const API_ENDPOINT = "https://api.weatherapi.com/v1";

let data = ref();
let error = ref();
let activeIndex = ref(0);

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
    <div class="panel-left"></div>
    <PanelRight
      :data
      :error
      :active-index="activeIndex"
      @select-index="(index) => (activeIndex = index)"
      @select-city="getCity"
    />
  </main>
</template>

<style scoped>
.main {
  display: flex;
  align-items: center;
}

.panel-left {
  width: 500px;
  height: 700px;
  border-radius: 30px;
  background: url("./assets/images/background.jpg") no-repeat -299px -267px;
}
</style>
