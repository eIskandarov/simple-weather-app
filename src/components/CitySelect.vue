<script setup>
import { onMounted, ref } from "vue";
import Button from "./Button.vue";
import IconLocation from "./icons/IconLocation.vue";
import Input from "./Input.vue";

const emit = defineEmits({
  "select-city"(payload) {
    return payload ? true : false;
  },
});

let isEdited = ref(false);
let city = ref("Moscow");

onMounted(() => {
  console.log("MOUNTED");
  emit("select-city", city.value);
});

function select() {
  isEdited.value = false;
  emit("select-city", city.value);
}

function edit() {
  isEdited.value = true;
}
</script>

<template>
  <div class="city-select">
    <div v-if="isEdited" class="city-input">
      <Input
        v-model="city"
        v-focus
        placeholder="Москва"
        @keyup.enter="select()"
      />
      <Button @click="select()">Сохранить</Button>
    </div>
    <Button v-if="!isEdited" @click="edit()">
      <IconLocation />
      Изменить город
    </Button>
  </div>
</template>

<style scoped>
.city-input {
  display: flex;
  column-gap: 12px;
}

.city-select {
  width: 420px;
}
</style>
