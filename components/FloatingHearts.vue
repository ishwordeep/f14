<script setup lang="ts">
const hearts = ref<{ id: number; left: string; size: string; duration: string; delay: string; emoji: string }[]>([])
let heartId = 0

const emojis = ['❤️', '💕', '💗', '💖', '💘', '🩷']

function spawnHeart() {
  const heart = {
    id: heartId++,
    left: `${Math.random() * 100}%`,
    size: `${0.8 + Math.random() * 1.5}rem`,
    duration: `${6 + Math.random() * 8}s`,
    delay: '0s',
    emoji: emojis[Math.floor(Math.random() * emojis.length)]
  }
  hearts.value.push(heart)

  // Remove heart after animation completes
  const totalTime = parseFloat(heart.duration) * 1000
  setTimeout(() => {
    hearts.value = hearts.value.filter((h) => h.id !== heart.id)
  }, totalTime)
}

onMounted(() => {
  // Spawn initial batch
  for (let i = 0; i < 8; i++) {
    setTimeout(() => spawnHeart(), i * 500)
  }
  // Then continuously spawn
  setInterval(spawnHeart, 2000)
})
</script>

<template>
  <div class="hearts-bg" aria-hidden="true">
    <div
      v-for="heart in hearts"
      :key="heart.id"
      class="heart"
      :style="{
        left: heart.left,
        fontSize: heart.size,
        animationDuration: heart.duration,
        animationDelay: heart.delay
      }"
    >
      {{ heart.emoji }}
    </div>
  </div>
</template>
