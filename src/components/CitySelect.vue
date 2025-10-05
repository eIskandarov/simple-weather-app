<script setup>
import Button from "./Button.vue";
import IconLocation from "./icons/IconLocation.vue";

const emit = defineEmits({
  selectCity(payload) {
    return payload ? true : false;
  },
});

function select() {
  emit("selectCity", "London");
}
</script>

<template>
  <Button @click="select()">
    <IconLocation />
    Изменить город
  </Button>
  <input />
  <Button>Сохранить</Button>
</template>

<style scoped></style>
