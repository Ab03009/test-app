<script setup lang="ts">
import type { Task } from '../types'

defineProps<{
  tasks: Task[]
}>()

const emit = defineEmits<{
  (e: 'updateTask', task: Task): void
}>()

const toggleTask = (task: Task) => {
  emit('updateTask', { ...task, done: !task.done })
}
</script>

<template>
  <div class="task-list">
    <div
      v-for="task in tasks"
      :key="task.id"
      class="task-item"
      :class="{ 'task-done': task.done }"
    >
      <label>
        <input
          type="checkbox"
          :checked="task.done"
          @change="toggleTask(task)"
        >
        {{ task.title }}
      </label>
    </div>
  </div>
</template>

<style scoped>
.task-list {
  background: white;
  border-radius: 8px;
  padding: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.task-item {
  padding: 0.75rem;
  border-bottom: 1px solid #eee;
  color: #000000;
}

.task-item:last-child {
  border-bottom: none;
}

.task-item label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
}

.task-item input[type="checkbox"] {
  width: 18px;
  height: 18px;
}

.task-done {
  text-decoration: line-through;
  color: #666666;
}
</style>