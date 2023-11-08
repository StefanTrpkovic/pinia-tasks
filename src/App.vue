<template>
  <main>
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo" />
      <h1>Pinia tasks</h1>
    </header>

    <div class="task-list">
      <div v-for="task in taskStore.tasks">
        <TaskDetails :task="task"/>
      </div>
    </div>    
  </main>
</template>

<script setup>
import { ref } from 'vue'
import { useTaskStore } from '@/stores/TaskStore'
import TaskDetails from '@/components/TaskDetails.vue'

const taskStore = ref(useTaskStore())
</script>
