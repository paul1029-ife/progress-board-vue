<script setup>
import { ref, onMounted } from 'vue'

const status = ref('active')
const name = ref('John Doe')
const tasks = ref([
  { id: 1, title: 'Task 1' },
  { id: 2, title: 'Task 2' },
  { id: 3, title: 'Task 3' },
])
const task = ref('')

const toggleStatus = () => {
  status.value = status.value === 'active' ? 'pending' : 'active'
}
const addTask = () => {
  const newTaskId = tasks.value.length + 1
  tasks.value.push({ id: newTaskId, title: `${task.value}` })
  task.value = ''
}

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await response.json()
    tasks.value = data.slice(0, 8).map((item) => ({ id: item.id, title: item.title }))
  } catch (error) {
    console.error('Error fetching tasks:', error)
  }
})
</script>

<template>
  <div class="app-container">
    <h1>Progress Board</h1>
    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'pending'">User is inactive</p>
    <p v-else>User status is unknown</p>

    <h3>{{ name }}</h3>

    <ul>
      <li v-for="task in tasks" :key="task.id">{{ task.title }}</li>
    </ul>
    <h3>Add a Task</h3>
    <p>Entered task {{ task }}</p>
    <div>
      <form @submit.prevent="addTask(task)">
        <input v-model="task" placeholder="Add a task" />
        <button>Add Task</button>
      </form>
      <button @click="toggleStatus">Toggle Status</button>
    </div>
  </div>
</template>

<style>
p {
  font-size: 16px;
  color: #333;
}
h3 {
  font-size: 20px;
  color: #007bff;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  padding: 5px 0;
  border-bottom: 1px solid #ccc;
}
button {
  margin-right: 10px;
  padding: 5px 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}
button:hover {
  background-color: #0056b3;
}
button:active {
  background-color: #004080;
}
.app-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  background-color: #f9f9f9;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
</style>
