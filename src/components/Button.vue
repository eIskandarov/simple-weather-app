<script setup></script>

<template>
  <button class="button">
    <slot></slot>
  </button>
</template>

<style scoped>
.button {
  display: flex;
  column-gap: 9px;
  width: 100%;
  justify-content: center;
  align-items: center;
  padding: 14px;
  font-size: 20px;
  font-weight: 500;
  border-radius: var(--default-border-radius);
  letter-spacing: 0.4px;
  border: none;
  color: var(--color-primary);
  background: var(--gradient);
  cursor: pointer;
}

.button:hover {
  background: var(--gradient-inverted);
}
</style>
