<script setup>
import IconRain from "./icons/weather/IconRain.vue";
import IconSun from "./icons/weather/IconSun.vue";
import IconCloud from "./icons/weather/IconCloud.vue";

const TEMPERATURE_MEASURE = "℃";
const { weatherCode, temperature, date } = defineProps({
  weatherCode: Number,
  temperature: Number,
  date: Date,
  isActive: Boolean,
});

function getIconColor(isActive) {
  return isActive ? "var(--color-primary-inverted)" : "var(--color-primary";
}
</script>

<template>
  <button type="button" class="day-card" :class="{ active: isActive }">
    <IconSun v-if="weatherCode <= 1003" :color="getIconColor(isActive)" />
    <IconRain
      v-if="weatherCode >= 1006 && weatherCode < 1063"
      :color="getIconColor(isActive)"
    />
    <IconCloud v-if="weatherCode >= 1063" :color="getIconColor(isActive)" />
    <div class="day-card__day">
      {{ date.toLocaleDateString("ru-RU", { weekday: "short" }) }}
    </div>
    <div class="day-card__temperature">
      {{ temperature }} {{ TEMPERATURE_MEASURE }}
    </div>
  </button>
</template>

<style scoped>
.day-card {
  font-size: 20px;
  display: flex;
  flex-direction: column;
  row-gap: 15px;
  align-items: center;
  justify-content: space-between;
  padding: 20px 24px;
  border-radius: 10px;
  border: none;
  color: var(--color-primary);
  background-color: var(--color-card-bg);
  cursor: pointer;
}

.day-card.active {
  background-color: var(--color-primary);
  color: var(--color-primary-inverted);
}

.day-card:not(.active):hover {
  background-color: #3a434f;
}

.day-card__day {
  font-style: normal;
  font-weight: 700;
}

.day-card__day::first-letter {
  text-transform: uppercase;
}

.day-card__temperature {
  font-style: normal;
  font-weight: 700;
}
</style>
