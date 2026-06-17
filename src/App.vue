<script setup>
import { ref, computed } from 'vue'
import TaskList from './components/TaskList.vue'

const tasks = ref([])
const newTaskText = ref('')
const filterMode = ref('all') 
let nextId = 1

function addTask() {
  const text = newTaskText.value.trim()
  if (!text) return
  tasks.value.push({ id: nextId++, text, completed: false })
  newTaskText.value = ''
}

function toggleTask(id) {
  const task = tasks.value.find(t => t.id === id)
  if (task) task.completed = !task.completed
}

function deleteTask(id) {
  tasks.value = tasks.value.filter(t => t.id !== id)
}

const filteredTasks = computed(() => {
  if (filterMode.value === 'active') return tasks.value.filter(t => !t.completed)
  if (filterMode.value === 'completed') return tasks.value.filter(t => t.completed)
  return tasks.value
})
</script>

<template>
  <div class="app">
    <h1>Список задач TO-DO List</h1>

    <div class="input-row">
      <input v-model="newTaskText" @keyup.enter="addTask" placeholder="Введіть задачу" />
      <button @click="addTask">Додати</button>
    </div>

    <div class="filters">
      <button :class="{ active: filterMode === 'all' }" @click="filterMode = 'all'">Всі</button>
      <button :class="{ active: filterMode === 'active' }" @click="filterMode = 'active'">Активні</button>
      <button :class="{ active: filterMode === 'completed' }" @click="filterMode = 'completed'">Виконані</button>
    </div>

    <TaskList :tasks="filteredTasks" @toggle="toggleTask" @delete="deleteTask" />
  </div>
</template>

<style>
.app { max-width: 480px; margin: 40px auto; padding: 24px; background: #1e1e2e; border-radius: 12px; color: #fff; font-family: sans-serif; }
.input-row { display: flex; gap: 8px; margin-bottom: 16px; }
.input-row input { flex: 1; padding: 8px; border-radius: 6px; border: none; }
.filters { display: flex; gap: 8px; margin-bottom: 16px; }
.filters button { padding: 6px 12px; border: none; border-radius: 6px; background: #333; color: #fff; cursor: pointer; }
.filters button.active { background: #8b5cf6; }
</style>
