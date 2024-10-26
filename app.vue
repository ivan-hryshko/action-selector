<template>
  <div class="main">
    <div class="container">
      <div
        v-if="isListSelected && isSelectActivityMode"
        class="actions-list"
      >
        <div
          v-for="action in selectedActions"
          :key="action"
          class="action"
          :class="actionClassOptions(action)"
          @click="selectActivity(action)"
        >
          {{ action }}
        </div>
      </div>
      <div
        v-else-if="isListSelected"
        class="actions-list"
      >
        <div
          v-for="action in actionsList[selectedListIndex].actions"
          :key="action"
          class="action"
          :class="actionClassOptions(action)"
          @click="selectActivity(action)"
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
          v-if="isListSelected && !isSelectActivityMode"
          class="action"
          @click="startSelectActivity"
        >
          Обрати активність
        </div>
        <div
          v-if="isListSelected && isSelectActivityMode"
          class="action"
          @click="nextIteration"
        >
          Далі
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const selectedListIndex = ref(null)
const isSelectActivityMode = ref(false)
const selectedActions = ref([])
const selectedActionsNext = ref([])

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

function startSelectActivity() {
  isSelectActivityMode.value = true
  selectedActions.value = actionsList.value[selectedListIndex.value].actions
}

function selectActivity(action) {
  if (!isSelectActivityMode.value) return
  selectedActionsNext.value.push(action)
}

function actionClassOptions(action) {
  return {
    'action--selected': selectedActionsNext.value.includes(action)
  }
}

function nextIteration() {
  selectedActions.value = selectedActionsNext.value
  selectedActionsNext.value = []
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

  &.action--selected {
    background-color: rgb(153, 243, 252);
  }
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
