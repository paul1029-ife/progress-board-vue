<script setup>
import { ref, onMounted } from 'vue'
import logo from '@/assets/logo.png'
</script>

<template>
  <nav
    class="bg-emerald-500 text-white h-15 flex items-center justify-between px-3 mx-5 rounded-lg"
  >
    <div class="flex gap-2">
      <img :src="logo" class="w-7 h-7 hover:scale-110 transition-all" />
      <p class="text-xl font-bold">Restate</p>
    </div>
    <div class="flex gap-7">
      <a class="text-lg hover:-translate-y-2 transition-all cursor-pointer">Home</a>
      <a class="text-lg hover:-translate-y-2 transition-all cursor-pointer">Boards</a>
      <a class="text-lg hover:-translate-y-2 transition-all cursor-pointer">Pricing</a>
      <a class="text-lg hover:-translate-y-2 transition-all cursor-pointer">Contact</a>
    </div>
    <div>
      <button class="bg-indigo-400 px-3 py-2 rounded-lg">Create Account</button>
    </div>
  </nav>
</template>
