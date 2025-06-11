<script setup>
import Navbar from './components/Navbar.vue'
import { RouterView } from 'vue-router'
</script>

<template>
  <div class="bg-gray-300 min-h-screen pt-6 flex flex-col gap-8">
    <Navbar />
    <RouterView />
  </div>
</template>
