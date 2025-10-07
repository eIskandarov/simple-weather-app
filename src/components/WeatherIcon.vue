<script setup>
import IconRain from "./icons/weather/IconRain.vue";
import IconSun from "./icons/weather/IconSun.vue";
import IconCloud from "./icons/weather/IconCloud.vue";

const { weatherCode, color = "var(--color-primary-inverted)" } = defineProps({
  weatherCode: Number,
  color: String,
});
</script>

<template>
  <IconSun v-if="weatherCode <= 1003" :color="color" />
  <IconRain v-if="weatherCode >= 1006 && weatherCode < 1063" :color="color" />
  <IconCloud v-if="weatherCode >= 1063" :color="color" />
</template>

<style scoped></style>
