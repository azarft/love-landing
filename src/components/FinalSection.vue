<template>
  <section class="section full finale" :id="id">
    <div class="finale-bg"></div>
    <div class="finale-petals" aria-hidden="true">
      <span v-for="n in 18" :key="`fp-${n}`" class="petal"></span>
    </div>
    <div class="finale-butterflies" aria-hidden="true">
      <span v-for="n in 6" :key="`fb-${n}`" class="butterfly"></span>
    </div>
    <div class="finale-content">
      <h2 class="finale-title glow-text">
        Мээрим, сен менин жашоомсуң.
        <br />
        Сени түбөлүк сүйөм.
        <br />
        — Дастан ❤️
      </h2>
    </div>
  </section>
</template>

<script setup>
import { onMounted, defineProps } from "vue";
import { gsap } from "gsap";

defineProps({
  id: { type: String, default: "" },
});

onMounted(() => {
  gsap.to(".finale-bg", {
    scale: 1.1,
    duration: 12,
    ease: "sine.inOut",
    repeat: -1,
    yoyo: true,
  });
});
</script>

<style scoped>
.finale {
  background: #160b16;
  color: #fff;
  overflow: hidden;
}

.finale-bg {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 30% 20%, rgba(255, 157, 206, 0.2), transparent 55%),
    radial-gradient(circle at 80% 80%, rgba(214, 189, 255, 0.25), transparent 60%),
    linear-gradient(120deg, #160b16, #2a0f2a, #1b0c1e);
  transform: scale(1.02);
}

.finale-content {
  position: relative;
  z-index: 2;
  text-align: center;
  max-width: 880px;
  padding: 0 20px;
}

.finale-title {
  font-family: "Playfair Display", serif;
  font-size: clamp(2.4rem, 5vw, 4rem);
  line-height: 1.4;
  color: #ffe6f2;
}

.finale-petals,
.finale-butterflies {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.petal {
  position: absolute;
  width: 14px;
  height: 20px;
  background: radial-gradient(circle at 30% 30%, #fff, #ffb4d9);
  border-radius: 60% 60% 80% 80%;
  opacity: 0.8;
  animation: fall 10s linear infinite;
}

.petal:nth-child(odd) {
  animation-duration: 12s;
}

.petal:nth-child(1) {
  left: 10%;
  top: -10%;
}
.petal:nth-child(2) {
  left: 20%;
  top: -20%;
}
.petal:nth-child(3) {
  left: 35%;
  top: -15%;
}
.petal:nth-child(4) {
  left: 50%;
  top: -18%;
}
.petal:nth-child(5) {
  left: 65%;
  top: -22%;
}
.petal:nth-child(6) {
  left: 80%;
  top: -16%;
}
.petal:nth-child(7) {
  left: 90%;
  top: -25%;
}
.petal:nth-child(8) {
  left: 12%;
  top: -30%;
}
.petal:nth-child(9) {
  left: 28%;
  top: -35%;
}
.petal:nth-child(10) {
  left: 42%;
  top: -28%;
}
.petal:nth-child(11) {
  left: 58%;
  top: -32%;
}
.petal:nth-child(12) {
  left: 72%;
  top: -20%;
}
.petal:nth-child(13) {
  left: 86%;
  top: -26%;
}
.petal:nth-child(14) {
  left: 6%;
  top: -22%;
}
.petal:nth-child(15) {
  left: 48%;
  top: -30%;
}
.petal:nth-child(16) {
  left: 68%;
  top: -14%;
}
.petal:nth-child(17) {
  left: 78%;
  top: -34%;
}
.petal:nth-child(18) {
  left: 92%;
  top: -18%;
}

.butterfly {
  position: absolute;
  width: 26px;
  height: 26px;
  background: radial-gradient(circle at 30% 30%, #fff, #e7c8ff);
  clip-path: polygon(50% 0%, 80% 20%, 100% 50%, 80% 80%, 50% 100%, 20% 80%, 0% 50%, 20% 20%);
  opacity: 0.8;
  animation: flutter 8s ease-in-out infinite;
}

.butterfly:nth-child(1) {
  left: 20%;
  top: 30%;
}
.butterfly:nth-child(2) {
  left: 70%;
  top: 20%;
}
.butterfly:nth-child(3) {
  left: 80%;
  top: 60%;
}
.butterfly:nth-child(4) {
  left: 30%;
  top: 65%;
}
.butterfly:nth-child(5) {
  left: 55%;
  top: 40%;
}
.butterfly:nth-child(6) {
  left: 10%;
  top: 50%;
}

@keyframes fall {
  0% {
    transform: translateY(0) rotate(0deg);
  }
  100% {
    transform: translateY(120vh) rotate(180deg);
  }
}
</style>
