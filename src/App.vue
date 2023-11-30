<script setup>
import { computed, ref } from 'vue'
import CardTask from './components/CardTask.vue'

const tareas = ref([
  {
    id: 1,
    title: 'Tarea 1',
    stage: 1
  },
  {
    id: 2,
    title: 'Tarea 2',
    stage: 3
  },
  {
    id: 3,
    title: 'Tarea 3',
    stage: 1
  }
])

const tareasStage1 = computed(() => tareas.value.filter((tarea) => tarea.stage === 1))
const tareasStage2 = computed(() => tareas.value.filter((tarea) => tarea.stage === 2))
const tareasStage3 = computed(() => tareas.value.filter((tarea) => tarea.stage === 3))

// logica del drag and drop
const dragStart = (event, tarea) => {
  event.dataTransfer.dropEffect = 'move'
  event.dataTransfer.effectAllowed = 'move'
  event.dataTransfer.setData('tareaId', tarea.id)
}

const onDrop = (event, list) => {
  const tareaId = event.dataTransfer.getData('tareaId')
  const tarea = tareas.value.find((tarea) => tarea.id === parseInt(tareaId))
  tarea.stage = list
}
</script>

<template>
  <main class="app-container">
    <h1>Kanban Board</h1>
    <div class="kanban-container">
      <div class="kanban-column" @drop="onDrop($event, 1)" @dragover.prevent @dragenter.prevent>
        <h1>Stage 1</h1>
        <CardTask
          v-for="tarea in tareasStage1"
          :key="tarea.id"
          :title="tarea.title"
          draggable="true"
          @dragstart="dragStart($event, tarea)"
        />
      </div>
      <div class="kanban-column" @drop="onDrop($event, 2)" @dragover.prevent @dragenter.prevent>
        <h1>Stage 2</h1>
        <CardTask
          v-for="tarea in tareasStage2"
          :key="tarea.id"
          :title="tarea.title"
          draggable="true"
          @dragstart="dragStart($event, tarea)"
        />
      </div>
      <div class="kanban-column" @drop="onDrop($event, 3)" @dragover.prevent @dragenter.prevent>
        <h1>Stage 3</h1>
        <CardTask
          v-for="tarea in tareasStage3"
          :key="tarea.id"
          :title="tarea.title"
          draggable="true"
          @dragstart="dragStart($event, tarea)"
        />
      </div>
    </div>
  </main>
</template>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  gap: 5px;
  height: 100dvh;
  justify-content: center;
  align-items: center;
}
.kanban-container {
  display: flex;
  gap: 50px;
  border: 2px solid black;
  border-radius: 8px;
  padding: 10px 20px 10px 20px;
  height: 50%;

  & .kanban-column {
    display: flex;
    flex-direction: column;
    max-width: 200px;
    gap: 10px;

    & h1 {
      font-weight: bold;
    }
  }
}
</style>
