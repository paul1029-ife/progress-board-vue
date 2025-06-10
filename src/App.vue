<script>
export default {
  data() {
    return {
      name: 'Progress Board',
      status: 'active',
      tasks: [
        { id: 1, title: 'Task 1', completed: true },
        { id: 2, title: 'Task 2', completed: false },
        { id: 3, title: 'Task 3', completed: true },
      ],
    }
  },
}
</script>

<template>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is inactive</p>
  <p v-else>User status is unknown</p>

  <h3>{{ name }}</h3>
  <ul>
    <li v-for="task in tasks" :key="task.id">{{ task.title }}</li>
  </ul>
  <button @click="status = 'pending'">Set Inactive</button>
  <button @click="status = 'active'">Set Active</button>
  <button @click="status = 'unknown'">Set Unknown</button>
</template>

<style></style>
