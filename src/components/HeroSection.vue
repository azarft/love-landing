<template>
  <section class="section full hero" id="hero">
    <div class="hero-bg"></div>
    <div class="hero-glow"></div>
    <div class="hero-particles" aria-hidden="true">
      <span v-for="n in 12" :key="`p-${n}`" class="particle"></span>
    </div>
    <div class="hero-floaters" aria-hidden="true">
      <span v-for="n in 8" :key="`f-${n}`" class="floater"></span>
      <span v-for="n in 6" :key="`b-${n}`" class="butterfly"></span>
    </div>
    <div class="hero-flowers" aria-hidden="true">
      <span v-for="n in 10" :key="`hf-${n}`" class="bloom"></span>
    </div>
    <div class="hero-content glass">
      <h1 class="hero-title glow-text">Мээрим</h1>
      <div class="soft-divider"></div>
      <p class="hero-sub">Бул барак сен үчүн гана...</p>
      <button class="primary-btn floating-btn no-heart" @click="$emit('open')">
        Ач
      </button>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from "vue";
import { gsap } from "gsap";

onMounted(() => {
  gsap.from(".hero-content", {
    y: 40,
    opacity: 0,
    duration: 1.6,
    ease: "power3.out",
  });
  gsap.to(".hero-glow", {
    opacity: 1,
    duration: 2,
    ease: "sine.out",
  });
});
</script>

<style scoped>
.hero {
  position: relative;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 20% 20%, #ffeef9, transparent 55%),
    radial-gradient(circle at 80% 10%, #f2e6ff, transparent 50%),
    linear-gradient(135deg, #ffe3f4, #f7e7ff, #fff7e0);
  animation: heroShift 18s ease-in-out infinite;
}

.hero-glow {
  position: absolute;
  inset: 10%;
  background: radial-gradient(circle, rgba(255, 191, 224, 0.45), transparent 70%);
  filter: blur(40px);
  opacity: 0;
}

.hero-content {
  position: relative;
  padding: 56px 32px;
  text-align: center;
  max-width: 520px;
  z-index: 2;
}

.hero-title {
  font-family: "Playfair Display", serif;
  font-size: clamp(3rem, 7vw, 5rem);
  margin: 0;
  color: #3a1b33;
}

.hero-sub {
  font-size: clamp(1rem, 2.6vw, 1.4rem);
  margin-bottom: 32px;
}

.hero-particles,
.hero-floaters,
.hero-flowers {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.particle {
  position: absolute;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.7);
  box-shadow: 0 0 25px rgba(255, 193, 221, 0.8);
  animation: particleFloat 6s ease-in-out infinite;
}

.particle:nth-child(odd) {
  width: 5px;
  height: 5px;
}

.particle:nth-child(1) {
  left: 10%;
  top: 20%;
}
.particle:nth-child(2) {
  left: 30%;
  top: 70%;
}
.particle:nth-child(3) {
  left: 60%;
  top: 30%;
}
.particle:nth-child(4) {
  left: 80%;
  top: 60%;
}
.particle:nth-child(5) {
  left: 50%;
  top: 10%;
}
.particle:nth-child(6) {
  left: 15%;
  top: 55%;
}
.particle:nth-child(7) {
  left: 70%;
  top: 15%;
}
.particle:nth-child(8) {
  left: 85%;
  top: 35%;
}
.particle:nth-child(9) {
  left: 40%;
  top: 50%;
}
.particle:nth-child(10) {
  left: 25%;
  top: 35%;
}
.particle:nth-child(11) {
  left: 65%;
  top: 75%;
}
.particle:nth-child(12) {
  left: 90%;
  top: 20%;
}

.floater,
.butterfly {
  position: absolute;
  width: 26px;
  height: 26px;
  border-radius: 50%;
  background: radial-gradient(circle at 30% 30%, #fff, #ffcde5);
  opacity: 0.8;
  filter: blur(0.5px);
  animation: floaty 8s ease-in-out infinite;
}

.floater::after {
  content: "";
  position: absolute;
  inset: 6px;
  border-radius: 50% 50% 0 50%;
  background: rgba(255, 201, 226, 0.8);
  transform: rotate(45deg);
}

.butterfly {
  background: radial-gradient(circle at 30% 30%, #fff, #e6ccff);
  clip-path: polygon(50% 0%, 80% 20%, 100% 50%, 80% 80%, 50% 100%, 20% 80%, 0% 50%, 20% 20%);
  animation: flutter 7s ease-in-out infinite;
}

.floater:nth-child(1) {
  left: 12%;
  top: 40%;
}
.floater:nth-child(2) {
  left: 20%;
  top: 70%;
}
.floater:nth-child(3) {
  left: 70%;
  top: 25%;
}
.floater:nth-child(4) {
  left: 80%;
  top: 50%;
}
.floater:nth-child(5) {
  left: 35%;
  top: 18%;
}
.floater:nth-child(6) {
  left: 55%;
  top: 70%;
}
.floater:nth-child(7) {
  left: 90%;
  top: 30%;
}
.floater:nth-child(8) {
  left: 45%;
  top: 85%;
}

.butterfly:nth-child(9) {
  left: 18%;
  top: 28%;
}
.butterfly:nth-child(10) {
  left: 65%;
  top: 12%;
}
.butterfly:nth-child(11) {
  left: 78%;
  top: 75%;
}
.butterfly:nth-child(12) {
  left: 40%;
  top: 55%;
}
.butterfly:nth-child(13) {
  left: 55%;
  top: 35%;
}
.butterfly:nth-child(14) {
  left: 28%;
  top: 80%;
}

.hero-flowers .bloom {
  position: absolute;
  width: 34px;
  height: 34px;
  border-radius: 50%;
  background: radial-gradient(circle at 30% 30%, #fff, #f7c6e4);
  box-shadow: 0 0 22px rgba(255, 170, 210, 0.7);
  opacity: 0.7;
  animation: bloomSpin 10s ease-in-out infinite;
}

.hero-flowers .bloom::after,
.hero-flowers .bloom::before {
  content: "";
  position: absolute;
  inset: 7px;
  border-radius: 50%;
  background: radial-gradient(circle at 30% 30%, #fff, #f1dcff);
}

.hero-flowers .bloom:nth-child(1) {
  left: 8%;
  top: 18%;
}
.hero-flowers .bloom:nth-child(2) {
  left: 20%;
  top: 70%;
}
.hero-flowers .bloom:nth-child(3) {
  left: 45%;
  top: 8%;
}
.hero-flowers .bloom:nth-child(4) {
  left: 65%;
  top: 30%;
}
.hero-flowers .bloom:nth-child(5) {
  left: 82%;
  top: 60%;
}
.hero-flowers .bloom:nth-child(6) {
  left: 55%;
  top: 75%;
}
.hero-flowers .bloom:nth-child(7) {
  left: 12%;
  top: 45%;
}
.hero-flowers .bloom:nth-child(8) {
  left: 72%;
  top: 12%;
}
.hero-flowers .bloom:nth-child(9) {
  left: 35%;
  top: 55%;
}
.hero-flowers .bloom:nth-child(10) {
  left: 90%;
  top: 28%;
}

@keyframes heroShift {
  0%,
  100% {
    filter: hue-rotate(0deg);
  }
  50% {
    filter: hue-rotate(12deg);
  }
}

@keyframes particleFloat {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

@keyframes flutter {
  0%,
  100% {
    transform: translateY(0) scale(1);
  }
  50% {
    transform: translateY(-16px) scale(1.08);
  }
}

@keyframes bloomSpin {
  0%,
  100% {
    transform: scale(1) rotate(0deg);
  }
  50% {
    transform: scale(1.15) rotate(12deg);
  }
}
</style>
