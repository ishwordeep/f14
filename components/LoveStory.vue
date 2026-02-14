<script setup lang="ts">
const steps = [
  { emoji: '✨', title: 'First Meet', text: 'The moment our paths crossed, everything changed. The universe had its own plans for us.' },
  { emoji: '🌸', title: 'Memories', text: 'Every laugh, every conversation, every shared silence — each became a treasure I hold close to my heart.' },
  { emoji: '💕', title: 'Today', text: 'Here we are, writing our story one beautiful day at a time. Every moment with you feels like a gift.' },
  { emoji: '♾️', title: 'Forever', text: 'This is not just a chapter — it\'s a never-ending story. My heart chose you, and it will always choose you.' }
]

const visibleSteps = ref<Set<number>>(new Set())
const stepRefs = ref<HTMLElement[]>([])

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        const index = Number(entry.target.getAttribute('data-index'))
        if (entry.isIntersecting) visibleSteps.value.add(index)
      })
    },
    { threshold: 0.3 }
  )
  stepRefs.value.forEach((el) => {
    if (el) observer.observe(el)
  })
})
</script>

<template>
  <section class="py-20 px-6">
    <h2 class="font-script text-4xl sm:text-5xl text-rose-600 text-center mb-16">Our Story</h2>

    <div class="max-w-3xl mx-auto relative">
      <!-- Timeline line -->
      <div class="timeline-line hidden sm:block"></div>

      <div
        v-for="(step, i) in steps"
        :key="i"
        ref="stepRefs"
        :data-index="i"
        class="relative mb-16 last:mb-0 transition-all duration-700"
        :class="[
          visibleSteps.has(i) ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10',
          i % 2 === 0 ? 'sm:pr-[55%]' : 'sm:pl-[55%]'
        ]"
        :style="{ transitionDelay: `${i * 150}ms` }"
      >
        <!-- Timeline dot -->
        <div
          class="hidden sm:flex absolute top-4 left-1/2 -translate-x-1/2 w-12 h-12 rounded-full bg-gradient-to-br from-rose-400 to-rose-600 items-center justify-center text-white text-lg shadow-lg z-10"
        >
          {{ step.emoji }}
        </div>

        <!-- Card -->
        <div class="bg-white/70 backdrop-blur-sm rounded-2xl p-8 shadow-lg hover:shadow-xl transition-shadow duration-300 border border-rose-100">
          <div class="sm:hidden text-3xl mb-3">{{ step.emoji }}</div>
          <h3 class="font-script text-2xl text-rose-600 mb-3">{{ step.title }}</h3>
          <p class="text-rose-500/80 font-light leading-relaxed">{{ step.text }}</p>
        </div>
      </div>
    </div>
  </section>
</template>
