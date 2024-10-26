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
}

.actions-list {
  display: flex;
  flex-direction: column;
  gap: 8px;

  .action {
    padding: 8px;
    border: 1px solid rgb(180, 178, 178);
    border-radius: 4px;
  }
}

</style>
