<script setup lang="ts">
defineProps<{ name: string }>()
</script>

<template>
  <section class="min-h-screen flex flex-col items-center justify-center text-center px-6 relative overflow-hidden">
    <!-- Decorative floating hearts -->
    <div class="absolute top-20 left-10 text-4xl animate-float opacity-20">❤️</div>
    <div class="absolute top-32 right-16 text-3xl animate-float-slow opacity-15">💕</div>
    <div class="absolute bottom-32 left-20 text-2xl animate-float opacity-10">💗</div>
    <div class="absolute bottom-20 right-10 text-5xl animate-float-slow opacity-15">❤️</div>

    <!-- Main content -->
    <div class="animate-fade-up">
      <p class="text-rose-400 text-lg mb-4 tracking-widest uppercase font-light">Happy Valentine's Day</p>
      <h1 class="font-script text-6xl sm:text-7xl md:text-8xl text-rose-600 mb-6 leading-tight">
        For {{ name }} ❤️
      </h1>
      <p class="text-rose-400 text-xl sm:text-2xl font-light max-w-lg mx-auto">
        A little story written with love
      </p>
    </div>

    <!-- Scroll indicator -->
    <div class="absolute bottom-10 animate-bounce">
      <div class="text-rose-300 text-sm mb-2">scroll down</div>
      <div class="text-rose-400 text-2xl">↓</div>
    </div>
  </section>
</template>
