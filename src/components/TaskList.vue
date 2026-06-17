<script setup>
import TaskItem from './TaskItem.vue'

defineProps({
  tasks: { type: Array, required: true }
})
defineEmits(['toggle', 'delete'])
</script>

<template>
  <ul class="task-list">
    <TaskItem
      v-for="task in tasks"
      :key="task.id"
      :task="task"
      @toggle="$emit('toggle', task.id)"
      @delete="$emit('delete', task.id)"
    />
  </ul>
</template>

<style scoped>
.task-list { list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap:10px; }
</style>