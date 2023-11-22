<script setup>
import { ref } from 'vue';
import Toggle from './components/toggle.vue'

const darkMode = ref(false);

function popup() {
  alert(darkMode.value);
}
</script>

<template>
  <div :class="{ 'dark' : darkMode }">
    <div class="bg-white dark:bg-black">
      <input v-model="darkMode" type="checkbox" id="dark-mode" name="darkMode">
      <Toggle v-model:value="darkMode"/>
      <div class="text-3xl text-white font-bold underline">
        My Potofolio
      </div>
      <button @click="popup">Click</button>
    </div>
  </div>
</template>

<style scoped>
</style>
