<template>
  <div class="app" @click="spawnHeart">
    <MusicToggle />
    <PhotoDecorations />
    <HeroSection @open="scrollToSection('confession')" />
    <ConfessionSection id="confession" />
    <PromiseSection id="promise" />
    <SecretLoveSection id="secret" />
    <FinalSection id="final" />
    <div ref="heartsLayer" class="hearts-layer" aria-hidden="true"></div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { gsap } from "gsap";
import HeroSection from "./components/HeroSection.vue";
import ConfessionSection from "./components/ConfessionSection.vue";
import PhotoDecorations from "./components/PhotoDecorations.vue";
import PromiseSection from "./components/PromiseSection.vue";
import FinalSection from "./components/FinalSection.vue";
import SecretLoveSection from "./components/SecretLoveSection.vue";
import MusicToggle from "./components/MusicToggle.vue";

const heartsLayer = ref(null);

const scrollToSection = (id) => {
  const target = document.getElementById(id);
  if (target) {
    target.scrollIntoView({ behavior: "smooth", block: "start" });
  }
};

const spawnHeart = (event) => {
  const target = event.target;
  if (target.closest(".no-heart")) return;
  if (!heartsLayer.value) return;
  const heart = document.createElement("div");
  heart.className = "floating-heart";
  const size = 10 + Math.random() * 18;
  const x = event.clientX - size / 2;
  const y = event.clientY - size / 2;
  heart.style.left = `${x}px`;
  heart.style.top = `${y}px`;
  heart.style.width = `${size}px`;
  heart.style.height = `${size}px`;
  heartsLayer.value.appendChild(heart);
  gsap.to(heart, {
    y: -120 - Math.random() * 80,
    x: `+=${-30 + Math.random() * 60}`,
    opacity: 0,
    scale: 1.6,
    duration: 1.6,
    ease: "power2.out",
    onComplete: () => heart.remove(),
  });
};
</script>
