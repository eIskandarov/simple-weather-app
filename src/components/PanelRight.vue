<script setup>
import { computed } from "vue";
import Error from "./Error.vue";
import DayCard from "./DayCard.vue";
import CitySelect from "./CitySelect.vue";
import Stat from "./Stat.vue";

const emit = defineEmits(["select-index", "select-city"]);

const { error, data, activeIndex } = defineProps({
  error: Object,
  data: Object,
  activeIndex: Number,
});

const statData = computed(() => {
  if (!data) {
    return [];
  }
  return [
    {
      label: "Влажность",
      stat: data.current.humidity + "%",
    },
    {
      label: "Облачность",
      stat: data.current.cloud + "%",
    },
    {
      label: "Ветер",
      stat: data.current.wind_kph + " км/ч",
    },
  ];
});

const errorMap = new Map([[1006, "Указанный город не найден"]]);
const errorDisplay = computed(() => {
  return errorMap.get(error?.error?.code);
});
</script>

<template>
  <div class="panel-right">
    <Error v-if="error" :error="errorDisplay" />

    <div v-if="data?.current">
      <div class="stat-list">
        <Stat v-for="item in statData" v-bind="item" :key="item.label" />
      </div>
      <div class="day-card-list">
        <DayCard
          v-for="(item, index) in data.forecast.forecastday"
          :key="item.date"
          :is-active="activeIndex === index"
          :weather-code="item.day.condition.code"
          :temperature="item.day.avgtemp_c"
          :date="new Date(item.date)"
          @click="() => emit('select-index', index)"
        />
      </div>
    </div>

    <CitySelect @select-city="(city) => emit('select-city', city)" />
  </div>
</template>

<style scoped>
.panel-right {
  display: flex;
  flex-direction: column;
  row-gap: 80px;
  background-color: var(--color-bg-main);
  padding: 60px 50px;
  border-radius: 25px;
  max-height: 650px;
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
