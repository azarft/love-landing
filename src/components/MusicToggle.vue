<template>
  <button class="music-toggle primary-btn no-heart" @click="toggleMusic">
    {{ isPlaying ? "Музыканы өчүрүү" : "Музыканы күйгүзүү" }}
  </button>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const isPlaying = ref(false);
let audioEl;

const setupAudio = () => {
  if (audioEl) return;
  audioEl = new Audio("/music/meerim.mp3");
  audioEl.loop = true;
  audioEl.volume = 0.45;
};

const toggleMusic = async () => {
  setupAudio();
  if (!audioEl) return;
  isPlaying.value = !isPlaying.value;
  if (isPlaying.value) {
    if (audioEl.readyState >= 2) {
      audioEl.currentTime = 43;
    } else {
      audioEl.addEventListener(
        "loadedmetadata",
        () => {
          audioEl.currentTime = 43;
        },
        { once: true }
      );
    }
    await audioEl.play();
  } else {
    audioEl.pause();
  }
};

const boostVolume = (event) => {
  if (!audioEl || !isPlaying.value) return;
  const level = event.detail?.level ?? 0.12;
  const nextVolume = Math.min(0.85, 0.45 + level);
  audioEl.volume = nextVolume;
  setTimeout(() => {
    if (isPlaying.value) audioEl.volume = 0.45;
  }, 2000);
};

onMounted(() => {
  window.addEventListener("music-boost", boostVolume);
});

onBeforeUnmount(() => {
  window.removeEventListener("music-boost", boostVolume);
  if (audioEl) audioEl.pause();
});
</script>

<style scoped>
.music-toggle {
  position: fixed;
  right: 20px;
  top: 20px;
  z-index: 70;
  font-size: 0.9rem;
  padding: 10px 20px;
}

@media (max-width: 600px) {
  .music-toggle {
    right: 12px;
    top: 12px;
    padding: 8px 16px;
  }
}
</style>
