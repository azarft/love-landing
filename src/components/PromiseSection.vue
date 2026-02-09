<template>
  <section class="section promise" :id="id">
    <div class="promise-bg" aria-hidden="true">
      <span v-for="n in 10" :key="`pf-${n}`" class="promise-flower"></span>
    </div>
    <div class="promise-card glass">
      <h2 class="section-title">Убада кылган жүрөк</h2>
      <ul class="promise-list">
        <li v-for="line in lines" :key="line">{{ line }}</li>
      </ul>
    </div>
  </section>
</template>

<script setup>
import { onMounted, defineProps } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

defineProps({
  id: { type: String, default: "" },
});

gsap.registerPlugin(ScrollTrigger);

const lines = [
  "Мен сага ар дайым кам көрөм.",
  "Мен сага таяныч болом.",
  "Мен сени урматтайм.",
  "Мен сенин колуңду эч качан коё бербейм.",
];

onMounted(() => {
  gsap.from(".promise-list li", {
    opacity: 0,
    y: 20,
    duration: 0.9,
    stagger: 0.4,
    ease: "power2.out",
    scrollTrigger: {
      trigger: ".promise-card",
      start: "top 80%",
    },
  });
});
</script>

<style scoped>
.promise {
  display: flex;
  justify-content: center;
  overflow: hidden;
}

.promise-card {
  padding: 48px 32px;
  max-width: 720px;
  width: 100%;
  position: relative;
  z-index: 2;
}

.promise-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 20px;
  font-size: clamp(1.1rem, 2.4vw, 1.35rem);
  color: #3a1b33;
}

.promise-bg {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.promise-flower {
  position: absolute;
  width: 32px;
  height: 32px;
  background: radial-gradient(circle at 30% 30%, #fff, #ffd0e8);
  border-radius: 50%;
  opacity: 0.6;
  filter: blur(0.2px);
  animation: floaty 8s ease-in-out infinite;
}

.promise-flower::after {
  content: "";
  position: absolute;
  inset: 8px;
  background: #fff;
  border-radius: 50%;
}

.promise-flower:nth-child(1) {
  left: 10%;
  top: 20%;
}
.promise-flower:nth-child(2) {
  left: 80%;
  top: 30%;
}
.promise-flower:nth-child(3) {
  left: 60%;
  top: 70%;
}
.promise-flower:nth-child(4) {
  left: 25%;
  top: 60%;
}
.promise-flower:nth-child(5) {
  left: 45%;
  top: 15%;
}
.promise-flower:nth-child(6) {
  left: 85%;
  top: 75%;
}
.promise-flower:nth-child(7) {
  left: 5%;
  top: 50%;
}
.promise-flower:nth-child(8) {
  left: 70%;
  top: 45%;
}
.promise-flower:nth-child(9) {
  left: 35%;
  top: 80%;
}
.promise-flower:nth-child(10) {
  left: 55%;
  top: 35%;
}
</style>
