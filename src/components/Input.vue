<script setup>
const data = defineModel({ type: String, required: true });
</script>

<template>
  <input v-model="data" type="text" class="input" />
</template>

<style scoped>
.input {
  font-size: 18px;
  max-width: 260px;
  padding: 15px 20px;
  color: var(--color-primary);
  border: none;
  border-radius: var(--default-border-radius);
  background-color: var(--color-card-bg);
  box-shadow: 1px 2px 4px 0px var(--color-bg-main);
}

.input::placeholder {
  color: var(--color-text-placeholder);
}
</style>
