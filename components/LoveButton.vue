<script setup lang="ts">
const props = defineProps<{ name: string }>()

const clicked = ref(false)
const buttonRef = ref<HTMLElement>()
const particles = ref<{ id: number; x: number; y: number; tx: string; ty: string }[]>([])

let particleId = 0

function handleClick() {
  clicked.value = true
  burstHearts()
}

function burstHearts() {
  const newParticles: typeof particles.value = []
  for (let i = 0; i < 15; i++) {
    const angle = (i / 15) * Math.PI * 2
    const distance = 80 + Math.random() * 80
    newParticles.push({
      id: particleId++,
      x: 0,
      y: 0,
      tx: `${Math.cos(angle) * distance}px`,
      ty: `${Math.sin(angle) * distance}px`
    })
  }
  particles.value = newParticles

  setTimeout(() => {
    particles.value = []
  }, 1200)
}
</script>

<template>
  <section class="py-20 px-6 text-center">
    <div class="relative inline-block">
      <!-- Burst particles -->
      <div
        v-for="p in particles"
        :key="p.id"
        class="heart-particle"
        :style="{ '--tx': p.tx, '--ty': p.ty }"
      >
        ❤️
      </div>

      <!-- Button (before click) -->
      <button
        v-if="!clicked"
        ref="buttonRef"
        class="sparkle-hover bg-gradient-to-r from-rose-400 to-rose-600 text-white font-body text-xl sm:text-2xl px-10 py-5 rounded-full shadow-xl hover:shadow-2xl transition-all duration-300 hover:scale-105 active:scale-95 animate-pulse-glow cursor-pointer"
        @click="handleClick"
      >
        Click if you love me ❤️
      </button>

      <!-- Message (after click) -->
      <div v-else class="animate-fade-up">
        <div class="text-6xl mb-6">💖</div>
        <h2 class="font-script text-4xl sm:text-5xl md:text-6xl text-rose-600 leading-tight">
          I love you {{ name }} forever
        </h2>
        <p class="text-rose-400 text-lg mt-4 font-light">and ever and ever... ♾️</p>

        <!-- Click again for more hearts -->
        <button
          class="mt-8 text-rose-400 hover:text-rose-600 transition-colors text-sm underline underline-offset-4 cursor-pointer"
          @click="burstHearts"
        >
          click for more hearts 💕
        </button>
      </div>
    </div>
  </section>
</template>
