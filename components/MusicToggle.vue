<script setup lang="ts">
const isPlaying = ref(false)
const audio = ref<HTMLAudioElement>()

function toggleMusic() {
  if (!audio.value) return

  if (isPlaying.value) {
    audio.value.pause()
  } else {
    audio.value.play().catch(() => {
      // Browser may block autoplay — ignore silently
    })
  }
  isPlaying.value = !isPlaying.value
}
</script>

<template>
  <div>
    <audio
      ref="audio"
      loop
      preload="none"
      src="https://cdn.pixabay.com/audio/2022/02/23/audio_ea70ad08e0.mp3"
    ></audio>

    <button
      class="music-btn"
      :title="isPlaying ? 'Pause music' : 'Play music'"
      @click="toggleMusic"
    >
      {{ isPlaying ? '⏸️' : '🎵' }}
    </button>
  </div>
</template>
