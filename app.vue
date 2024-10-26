<template>
  <div class="main">
    <div class="container">
      <div
        v-if="isListSelected"
        class="actions-list"
      >
        <div
          v-for="action in actionsList[selectedListIndex].actions"
          :key="action"
          class="action"
        >
          {{ action}}
        </div>
      </div>
      <div
        v-else
        class="actions-list"
      >
        <div
          v-for="(list, index) in actionsList"
          :key="list"
          class="action"
          @click="selectList(index)"
        >
          {{ list.name }}
        </div>
      </div>

      <div class="footer">
        <div
          v-if="isListSelected"
          class="action"
        >
          Обрати активність
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const selectedListIndex = ref(null)
const actionsList = ref([
  {
    name: 'today',
    actions: [
      'Вязати',
      'Гратись з кішкою',
      'Гратись з кішкою',
      'Вязати',
      'Гратись з кішкою',
    ]
  }
])

const isListSelected = computed(() => {
  return selectedListIndex.value === 0 || selectedListIndex.value > 0
})

function selectList(index) {
  console.log('index :>> ', index);
  selectedListIndex.value = index
}
</script>

<style lang="scss">
.main {
  display: flex;
  justify-content: center;
  background-color: #eafaff;
  height: 100vh;

  .container {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 300px;
    padding: 16px;
  }
}

.actions-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
  padding: 8px;
  overflow-y: auto;
}
// .actions-list {
//   display: grid;
//   grid-template-columns: auto auto;
//   grid-auto-rows: min-content;
//   gap: 8px;
//   padding: 8px;
//   overflow-y: auto;
// }
.action {
  padding: 8px;
  border: 1px solid rgb(180, 178, 178);
  border-radius: 4px;
  background-color: white;
}

.footer {
  display: flex;
  gap: 8px;
}

@media screen and (max-width: 768px) {
  .main {
    .container {
      width: 100%;
    }
  }

  .actions-list {
    grid-template-columns: 1fr 1fr;
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
