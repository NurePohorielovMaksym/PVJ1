<script setup>
defineProps({
  task: { type: Object, required: true }
})
defineEmits(['toggle', 'delete'])
</script>

<template>
  <li class="task-item">
    <div class="task-left" @click="$emit('toggle')">
      <span class="circle" :class="{ completed: task.completed }"></span>
      <span class="task-text" :class="{ completed: task.completed }">{{ task.text }}</span>
    </div>
    <button class="delete-btn" @click="$emit('delete')">Видалити</button>
  </li>
</template>

<style scoped>
.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 12px;
  border: 1px solid #2a2a3a;
  border-radius: 10px;
}
.task-left {
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
}
.circle {
  width: 16px;
  height: 16px;
  border-radius: 50%;
  border: 2px solid #666;
  display: inline-block;
  flex-shrink: 0;
}
.circle.completed {
  background: #8b5cf6;
  border-color: #8b5cf6;
}
.task-text.completed {
  text-decoration: line-through;
  opacity: 0.5;
}
.delete-btn {
  background: none;
  border: none;
  color: #888;
  cursor: pointer;
  font-size: 0.9em;
}
.delete-btn:hover {
  color: #fff;
}
</style>