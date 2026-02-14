<script setup lang="ts">
const quotes = [
  "In all the world, there is no heart for me like yours.",
  "Whatever our souls are made of, his and mine are the same.",
  "I have waited for this opportunity for more than half a century, to repeat to you once again my vow of eternal fidelity and everlasting love.",
  "You are my today and all of my tomorrows.",
  "I loved you yesterday, I love you still. I always have, I always will.",
  "Every love story is beautiful, but ours is my favorite.",
  "I look at you and see the rest of my life in front of my eyes.",
  "You are the finest, loveliest, tenderest, and most beautiful person I have ever known — and even that is an understatement."
]

const quote = quotes[Math.floor(Math.random() * quotes.length)]

const isVisible = ref(false)
const sectionRef = ref<HTMLElement>()

onMounted(() => {
  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) isVisible.value = true
    },
    { threshold: 0.3 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})
</script>

<template>
  <section
    ref="sectionRef"
    class="min-h-[60vh] flex items-center justify-center px-6 py-20"
  >
    <div
      class="max-w-2xl text-center transition-all duration-1000"
      :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'"
    >
      <div class="text-rose-300 text-4xl mb-6">✦</div>
      <blockquote class="font-script text-3xl sm:text-4xl md:text-5xl text-rose-600 leading-relaxed">
        "{{ quote }}"
      </blockquote>
    </div>
  </section>
</template>
