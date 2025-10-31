<script setup lang="ts">
import { RouterView } from 'vue-router'
import NavBar from './components/Navbar.vue'
</script>

<template>
  <div class="min-h-screen pt-6 flex flex-col gap-8">
    <NavBar />
    <RouterView />
  </div>
</template>
