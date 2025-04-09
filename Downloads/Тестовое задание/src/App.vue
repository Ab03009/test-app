<script setup lang="ts">
import { onMounted, ref } from 'vue'
import TaskList from './components/TaskList.vue'
import type { Task } from './types'

const tasks = ref<Task[]>([])
const loading = ref(true)

onMounted(async () => {
  // Try to load from localStorage first
  const savedTasks = localStorage.getItem('tasks')
  if (savedTasks) {
    tasks.value = JSON.parse(savedTasks)
    loading.value = false
    return
  }

  // If no saved tasks, load from JSON file
  try {
    const response = await fetch('/tasks.json')
    tasks.value = await response.json()
  } catch (error) {
    console.error('Error loading tasks:', error)
  } finally {
    loading.value = false
  }
})

const updateTask = (updatedTask: Task) => {
  const index = tasks.value.findIndex(t => t.id === updatedTask.id)
  if (index !== -1) {
    tasks.value[index] = updatedTask
    // Save to localStorage
    localStorage.setItem('tasks', JSON.stringify(tasks.value))
  }
}
</script>

<template>
  <div class="container">
    <h1>Список задач</h1>
    <div v-if="loading" class="loading">
      Загрузка задач...
    </div>
    <TaskList
      v-else
      :tasks="tasks"
      @update-task="updateTask"
    />
  </div>
</template>

<style>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
}

.loading {
  text-align: center;
  padding: 2rem;
  font-style: italic;
  color: #000000;
}

h1 {
  text-align: center;
  margin-bottom: 2rem;
  color: #000000;
}
</style>