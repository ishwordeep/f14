<script setup lang="ts">
const props = defineProps<{ name: string }>()

const message = computed(
  () =>
    `Dear ${props.name}, you are the reason my heart smiles. Every day with you feels like a beautiful dream I never want to wake up from. You make the ordinary feel extraordinary, and I am so grateful for every single moment we share. You are my favorite hello and my hardest goodbye. I hope you always know just how deeply, truly, and completely you are loved.`
)

const displayedText = ref('')
const isVisible = ref(false)
const sectionRef = ref<HTMLElement>()
const hasTyped = ref(false)

onMounted(() => {
  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting && !hasTyped.value) {
        isVisible.value = true
        hasTyped.value = true
        typeText()
      }
    },
    { threshold: 0.3 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})

function typeText() {
  const text = message.value
  let i = 0
  const interval = setInterval(() => {
    if (i < text.length) {
      displayedText.value += text[i]
      i++
    } else {
      clearInterval(interval)
    }
  }, 30)
}
</script>

<template>
  <section ref="sectionRef" class="py-20 px-6">
    <div class="max-w-2xl mx-auto text-center">
      <h2 class="font-script text-4xl sm:text-5xl text-rose-600 mb-10">A Message For You</h2>

      <div
        class="bg-white/60 backdrop-blur-sm rounded-2xl p-8 sm:p-12 shadow-lg border border-rose-100 min-h-[200px]"
      >
        <p class="text-rose-500/90 text-lg sm:text-xl font-light leading-relaxed text-left">
          <span>{{ displayedText }}</span>
          <span v-if="displayedText.length < message.length && isVisible" class="typing-cursor"></span>
        </p>
      </div>
    </div>
  </section>
</template>
