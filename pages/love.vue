<script setup lang="ts">
const route = useRoute()
const name = computed(() => (route.query.name as string) || 'My Love')
</script>

<template>
  <div class="min-h-screen bg-gradient-to-b from-blush via-rose-50 to-rose-100 font-body relative">
    <!-- Floating hearts background -->
    <FloatingHearts />

    <!-- Music toggle -->
    <MusicToggle />

    <!-- Content sections -->
    <div class="relative z-10">
      <HeroLove :name="name" />
      <LoveQuote />
      <LoveStory />
      <LoveMessage :name="name" />
      <LoveButton :name="name" />

      <!-- Footer -->
      <footer class="text-center py-10 text-rose-400 text-sm font-light">
        Made with ❤️ just for you
      </footer>
    </div>
  </div>
</template>
