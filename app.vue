<template>
  <div class="main">
    <div
      class="actions-list"
    >
      <div
        v-for="action in actionsList"
        :key="action"
        class="action"
      >
        {{ action }}
      </div>

    </div>
    <!-- <NuxtRouteAnnouncer />
    <NuxtWelcome /> -->
  </div>
</template>

<script setup>
import { ref } from 'vue';

const actionsList = ['Вязати', 'Гратись з кішкою']
</script>

<style lang="scss">
.main {
  display: flex;
  justify-content: center;
  background-color: #eafaff;
  height: 100vh;
}

.actions-list {
  display: grid;
  grid-template-columns: auto auto;
  grid-auto-rows: min-content;
  gap: 8px;
  padding: 8px;

  .action {
    padding: 8px;
    border: 1px solid rgb(180, 178, 178);
    border-radius: 4px;
    background-color: white;
  }
}

/* assets/css/reset.css */
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html, body {
  height: 100%;
  font-family: sans-serif;
}

img, picture, video, canvas, svg {
  display: block;
  max-width: 100%;
}

button, input, select, textarea {
  font-family: inherit;
}


</style>
