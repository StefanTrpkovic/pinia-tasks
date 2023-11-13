<template>
  <main>
    <!-- heading -->
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo" />
      <h1>Pinia tasks</h1>
    </header>

    <!-- new task form -->
    <div class="new-task-form">
      <TaskForm />
    </div>

    <!-- filter -->
    <nav class="filter">
      <button v-on:click="filter = 'all'">All tasks</button>
      <button v-on:click="filter = 'fav'">Fav tasks</button>
    </nav>

    <!-- loading -->
    <div class="loading" v-if="loading">Loading tasks...</div>

    <!-- task list -->
    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ totalCount }} tasks left to do</p>
      <div v-for="task in tasks">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="task-list" v-else>
      <p>You have {{ favCount }} favs left to do</p>
      <div v-for="task in favs">
        <TaskDetails :task="task" />
      </div>
    </div>

    <button @click="taskStore.$reset">Reset store</button>

  </main>
</template>

<script setup>
import { ref } from 'vue'
import { storeToRefs } from 'pinia'
import { useTaskStore } from '@/stores/TaskStore'
import TaskDetails from '@/components/TaskDetails.vue'
import TaskForm from '@/components/TaskForm.vue'

const taskStore = useTaskStore()
const { tasks, favs, loading, totalCount, favCount } = storeToRefs(taskStore)
taskStore.getTasks()

const filter = ref('all')


</script>
