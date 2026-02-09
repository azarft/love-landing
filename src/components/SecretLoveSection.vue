<template>
  <section class="section secret" :id="id">
    <button class="secret-btn primary-btn floating-btn no-heart" @click="openSecret">
      Мени бас
    </button>

    <div v-if="isOpen" class="secret-overlay no-heart" @click.self="closeSecret">
      <div ref="scene" class="secret-scene glass">
        <button class="close-btn no-heart" @click="closeSecret" aria-label="Жабуу">
          ×
        </button>
        <div class="secret-petals" aria-hidden="true">
          <span v-for="n in 18" :key="`sp-${n}`" class="petal"></span>
        </div>
        <div class="secret-flowers" aria-hidden="true">
          <span v-for="n in 12" :key="`sf-${n}`" class="flower"></span>
        </div>
        <h3 class="secret-title glow-text">Жашыруун сыр</h3>
        <p class="secret-text">
          Сен менин тагдырымсың.
          <br />
          Мен сени Аллах мага белек кылгандай сезем.
          <br />
          Сенсиз жашоомду элестете албайм.
          <br />
          Сени менен ар бир күн — бакыт.
        </p>
        <p class="secret-note">Аралык бар, бирок жүрөк ар дайым бирге.</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, defineProps } from "vue";
import { gsap } from "gsap";

defineProps({
  id: { type: String, default: "" },
});

const isOpen = ref(false);
const scene = ref(null);

const openSecret = () => {
  isOpen.value = true;
  window.dispatchEvent(new CustomEvent("music-boost", { detail: { level: 0.12 } }));
  requestAnimationFrame(() => {
    gsap.fromTo(
      ".secret-overlay",
      { opacity: 0 },
      { opacity: 1, duration: 1.2, ease: "power2.out" }
    );
    gsap.fromTo(
      scene.value,
      { scale: 0.96, y: 20 },
      { scale: 1, y: 0, duration: 1.4, ease: "power3.out" }
    );
    gsap.fromTo(
      ".secret-note",
      { opacity: 0, y: 10 },
      { opacity: 1, y: 0, duration: 1.2, delay: 0.8, ease: "power2.out" }
    );
  });
};

const closeSecret = () => {
  isOpen.value = false;
};

onMounted(() => {
  gsap.to(".secret-btn", {
    boxShadow: "0 0 25px rgba(255, 158, 207, 0.7)",
    duration: 2,
    yoyo: true,
    repeat: -1,
    ease: "sine.inOut",
  });
});
</script>

<style scoped>
.secret {
  display: grid;
  place-items: center;
  position: relative;
}

.secret-btn {
  font-size: 1.05rem;
}

.secret-overlay {
  position: fixed;
  inset: 0;
  background: radial-gradient(circle at 30% 20%, rgba(255, 232, 244, 0.7), rgba(156, 86, 128, 0.25)),
    linear-gradient(120deg, rgba(255, 244, 251, 0.85), rgba(255, 214, 236, 0.6));
  backdrop-filter: blur(8px);
  display: grid;
  place-items: center;
  z-index: 60;
}

.secret-scene {
  position: relative;
  padding: 48px 32px;
  max-width: 720px;
  width: min(90vw, 720px);
  text-align: center;
  color: #3a1b33;
  overflow: hidden;
}

.close-btn {
  position: absolute;
  top: 18px;
  right: 18px;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  border: none;
  background: rgba(255, 255, 255, 0.7);
  color: #3a1b33;
  font-size: 1.4rem;
  cursor: pointer;
  box-shadow: 0 8px 18px rgba(70, 20, 50, 0.2);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.close-btn:hover {
  transform: scale(1.05);
  box-shadow: 0 12px 24px rgba(70, 20, 50, 0.28);
}

.secret-title {
  margin: 0 0 16px;
  font-family: "Playfair Display", serif;
  font-size: 2rem;
}

.secret-text {
  margin: 0 0 24px;
  line-height: 1.8;
  font-size: 1.1rem;
}

.secret-note {
  margin-top: 14px;
  color: #4a2942;
  font-weight: 600;
}

.secret-petals {
  position: absolute;
  inset: 0;
  pointer-events: none;
  opacity: 0.7;
}

.secret-petals .petal {
  position: absolute;
  width: 12px;
  height: 18px;
  background: radial-gradient(circle at 30% 30%, #fff, #ffb4d9);
  border-radius: 60% 60% 80% 80%;
  animation: floaty 6s ease-in-out infinite;
}

.secret-petals .petal:nth-child(1) {
  left: 15%;
  top: 20%;
}
.secret-petals .petal:nth-child(2) {
  left: 35%;
  top: 10%;
}
.secret-petals .petal:nth-child(3) {
  left: 60%;
  top: 18%;
}
.secret-petals .petal:nth-child(4) {
  left: 80%;
  top: 28%;
}
.secret-petals .petal:nth-child(5) {
  left: 20%;
  top: 60%;
}
.secret-petals .petal:nth-child(6) {
  left: 45%;
  top: 70%;
}
.secret-petals .petal:nth-child(7) {
  left: 70%;
  top: 65%;
}
.secret-petals .petal:nth-child(8) {
  left: 85%;
  top: 60%;
}
.secret-petals .petal:nth-child(9) {
  left: 10%;
  top: 40%;
}
.secret-petals .petal:nth-child(10) {
  left: 50%;
  top: 40%;
}
.secret-petals .petal:nth-child(11) {
  left: 30%;
  top: 80%;
}
.secret-petals .petal:nth-child(12) {
  left: 70%;
  top: 85%;
}
.secret-petals .petal:nth-child(13) {
  left: 55%;
  top: 25%;
}
.secret-petals .petal:nth-child(14) {
  left: 90%;
  top: 42%;
}
.secret-petals .petal:nth-child(15) {
  left: 5%;
  top: 70%;
}
.secret-petals .petal:nth-child(16) {
  left: 38%;
  top: 52%;
}
.secret-petals .petal:nth-child(17) {
  left: 72%;
  top: 12%;
}
.secret-petals .petal:nth-child(18) {
  left: 95%;
  top: 55%;
}

.secret-flowers {
  position: absolute;
  inset: 0;
  pointer-events: none;
  opacity: 0.7;
}

.secret-flowers .flower {
  position: absolute;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  background: radial-gradient(circle at 30% 30%, #fff, #f7c6e4);
  box-shadow: 0 0 18px rgba(255, 176, 214, 0.6);
  animation: bloom 7s ease-in-out infinite;
}

.secret-flowers .flower::after,
.secret-flowers .flower::before {
  content: "";
  position: absolute;
  inset: 6px;
  border-radius: 50%;
  background: radial-gradient(circle at 30% 30%, #fff, #f5e1ff);
}

.secret-flowers .flower:nth-child(1) {
  left: 8%;
  top: 18%;
}
.secret-flowers .flower:nth-child(2) {
  left: 22%;
  top: 75%;
}
.secret-flowers .flower:nth-child(3) {
  left: 40%;
  top: 10%;
}
.secret-flowers .flower:nth-child(4) {
  left: 68%;
  top: 20%;
}
.secret-flowers .flower:nth-child(5) {
  left: 82%;
  top: 68%;
}
.secret-flowers .flower:nth-child(6) {
  left: 55%;
  top: 80%;
}
.secret-flowers .flower:nth-child(7) {
  left: 15%;
  top: 45%;
}
.secret-flowers .flower:nth-child(8) {
  left: 75%;
  top: 45%;
}
.secret-flowers .flower:nth-child(9) {
  left: 48%;
  top: 35%;
}
.secret-flowers .flower:nth-child(10) {
  left: 30%;
  top: 30%;
}
.secret-flowers .flower:nth-child(11) {
  left: 62%;
  top: 55%;
}
.secret-flowers .flower:nth-child(12) {
  left: 88%;
  top: 32%;
}

@keyframes bloom {
  0%,
  100% {
    transform: scale(1) rotate(0deg);
    opacity: 0.7;
  }
  50% {
    transform: scale(1.12) rotate(10deg);
    opacity: 1;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.6s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 600px) {
  .secret-scene {
    padding: 36px 22px;
  }
}
</style>
