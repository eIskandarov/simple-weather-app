<script setup>
const props = defineProps({
  error: String,
});
</script>

<template>
  <div v-if="props.error" class="error">{{ props.error }}</div>
</template>

<style scoped>
.error {
  --margin: 60px;
  font-size: 18px;
  padding: 15px;
  text-align: center;
  background-color: var(--color-card-bg);
  border-radius: 0px 0px 25px 25px;
  margin-top: calc(-1 * var(--margin));
  margin-bottom: var(--margin);
}
</style>
