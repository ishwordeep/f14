<script setup lang="ts">
const props = defineProps<{ name: string }>()

const lines = computed(() => [
  `My Dearest ${props.name},`,
  '',
  `You are the reason my heart smiles. Every day with you feels like a beautiful dream I never want to wake up from.`,
  '',
  `You make the ordinary feel extraordinary, and I am so grateful for every single moment we share. You are my favorite hello and my hardest goodbye.`,
  '',
  `I hope you always know just how deeply, truly, and completely you are loved.`,
  '',
  `Forever & Always Yours,`,
  `With all my love ❤️`
])

const displayedLines = ref<string[]>([])
const isVisible = ref(false)
const sectionRef = ref<HTMLElement>()
const hasTyped = ref(false)
const doneTyping = ref(false)

onMounted(() => {
  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting && !hasTyped.value) {
        isVisible.value = true
        hasTyped.value = true
        typeLines()
      }
    },
    { threshold: 0.2 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})

function typeLines() {
  let lineIdx = 0
  let charIdx = 0
  displayedLines.value = ['']

  const interval = setInterval(() => {
    const currentLine = lines.value[lineIdx]

    if (charIdx < currentLine.length) {
      displayedLines.value[lineIdx] += currentLine[charIdx]
      charIdx++
    } else {
      lineIdx++
      charIdx = 0
      if (lineIdx < lines.value.length) {
        displayedLines.value.push('')
      } else {
        doneTyping.value = true
        clearInterval(interval)
      }
    }
  }, 25)
}
</script>

<template>
  <section ref="sectionRef" class="py-20 px-6">
    <div class="max-w-2xl mx-auto text-center">
      <h2 class="font-script text-4xl sm:text-5xl text-rose-600 mb-10">A Message For You</h2>

      <!-- Letter paper -->
      <div
        class="relative bg-[#fffaf0] rounded-sm p-8 sm:p-12 shadow-[4px_4px_20px_rgba(0,0,0,0.1)] min-h-[350px] text-left border border-[#e8ddd0]"
        style="background-image: repeating-linear-gradient(transparent, transparent 31px, #e8ddd0 31px, #e8ddd0 32px); background-position: 0 40px;"
      >
        <!-- Red margin line -->
        <div class="absolute top-0 bottom-0 left-16 sm:left-20 w-[1px] bg-rose-300/50"></div>

        <!-- Letter content -->
        <div class="pl-6 sm:pl-10 font-script text-lg sm:text-xl text-rose-800/80 leading-[32px]">
          <template v-for="(line, i) in displayedLines" :key="i">
            <!-- Greeting line (first line) — bold -->
            <p
              v-if="i === 0"
              class="font-bold text-rose-700 text-xl sm:text-2xl mb-0"
              style="line-height: 32px;"
            >
              {{ line }}
              <span v-if="!doneTyping && i === displayedLines.length - 1" class="typing-cursor"></span>
            </p>

            <!-- Empty lines as spacing -->
            <p
              v-else-if="lines[i] === ''"
              style="line-height: 32px;"
            >&nbsp;</p>

            <!-- Closing lines (last 2) — italic right-aligned -->
            <p
              v-else-if="i >= lines.length - 2"
              class="italic text-right text-rose-600"
              style="line-height: 32px;"
            >
              {{ line }}
              <span v-if="!doneTyping && i === displayedLines.length - 1" class="typing-cursor"></span>
            </p>

            <!-- Body paragraphs -->
            <p
              v-else
              style="line-height: 32px;"
            >
              {{ line }}
              <span v-if="!doneTyping && i === displayedLines.length - 1" class="typing-cursor"></span>
            </p>
          </template>
        </div>

        <!-- Decorative stamp -->
        <div class="absolute top-4 right-4 sm:top-6 sm:right-6 w-14 h-14 sm:w-16 sm:h-16 border-2 border-dashed border-rose-300 rounded-sm flex items-center justify-center text-2xl sm:text-3xl opacity-60 rotate-6">
          💌
        </div>
      </div>
    </div>
  </section>
</template>
