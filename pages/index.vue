<script setup lang="ts">
// Redirect to /love with a default name
navigateTo({ path: '/love', query: { name: 'My Love' } })
</script>

<template>
  <div class="min-h-screen flex items-center justify-center bg-blush">
    <p class="text-rose-400 font-script text-2xl animate-pulse">Loading your love letter...</p>
  </div>
</template>
