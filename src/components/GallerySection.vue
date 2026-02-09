<template>
  <section class="section gallery" :id="id">
    <div class="gallery-header">
      <h2 class="section-title">Сенин сүрөттөрүң</h2>
      <p class="section-sub">Бул жерде Мээримдин назик көз ирмемдери.</p>
    </div>
    <div class="gallery-hearts" aria-hidden="true">
      <span v-for="n in 8" :key="`gh-${n}`" class="gallery-heart"></span>
    </div>
    <div ref="cardsWrap" class="gallery-cards">
      <article
        v-for="(image, index) in images"
        :key="image"
        class="gallery-card glass"
        @mousemove="tiltCard($event, index)"
        @mouseleave="resetCard(index)"
      >
        <div class="gallery-image" :style="`background-image: url(/${image})`"></div>
        <div class="gallery-overlay">
          <span>Сүрөт №{{ index + 1 }}</span>
        </div>
      </article>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, defineProps } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

defineProps({
  id: { type: String, default: "" },
});

gsap.registerPlugin(ScrollTrigger);

const images = ["image1.jpg", "image2.jpg", "image3.jpg", "image4.jpg"];
const cardsWrap = ref(null);

const tiltCard = (event, index) => {
  const card = cardsWrap.value?.children[index];
  if (!card) return;
  const rect = card.getBoundingClientRect();
  const x = event.clientX - rect.left;
  const y = event.clientY - rect.top;
  const rotateX = (y / rect.height - 0.5) * -10;
  const rotateY = (x / rect.width - 0.5) * 10;
  card.style.transform = `rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale(1.03)`;
};

const resetCard = (index) => {
  const card = cardsWrap.value?.children[index];
  if (card) card.style.transform = "rotateX(0deg) rotateY(0deg) scale(1)";
};

onMounted(() => {
  gsap.from(".gallery-card", {
    opacity: 0,
    y: 40,
    stagger: 0.2,
    duration: 1,
    ease: "power2.out",
    scrollTrigger: {
      trigger: ".gallery-cards",
      start: "top 80%",
    },
  });

  gsap.utils.toArray(".gallery-image").forEach((image) => {
    gsap.to(image, {
      backgroundPosition: "50% 60%",
      ease: "none",
      scrollTrigger: {
        trigger: image,
        start: "top bottom",
        end: "bottom top",
        scrub: true,
      },
    });
  });
});
</script>

<style scoped>
.gallery {
  overflow: hidden;
}

.gallery-header {
  text-align: center;
  margin-bottom: 40px;
}

.gallery-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 28px;
  position: relative;
  z-index: 2;
}

.gallery-card {
  padding: 18px;
  transition: transform 0.4s ease;
  transform-style: preserve-3d;
  border-radius: 22px;
  overflow: hidden;
  position: relative;
}

.gallery-image {
  height: 320px;
  border-radius: 18px;
  background-size: cover;
  background-position: center;
  box-shadow: inset 0 0 60px rgba(255, 255, 255, 0.2);
  transition: transform 0.6s ease;
}

.gallery-card:hover .gallery-image {
  transform: scale(1.05);
}

.gallery-overlay {
  position: absolute;
  inset: auto 22px 22px;
  padding: 10px 16px;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.7);
  font-size: 0.9rem;
  color: #3a1b33;
  box-shadow: 0 10px 20px rgba(75, 25, 59, 0.2);
}

.gallery-hearts {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.gallery-heart {
  position: absolute;
  width: 12px;
  height: 12px;
  background: radial-gradient(circle at 30% 30%, #fff, #ff9ecf);
  clip-path: path("M8.5,2 C7,0 4,0 2.5,1.5 C0.5,3.5 1,7 4.5,9.5 C8,7 15.5,3.5 13.5,1.5 C12,0 9,0 8.5,2 Z");
  opacity: 0.7;
  animation: heartFloat 6s ease-in-out infinite;
}

.gallery-heart:nth-child(1) {
  left: 5%;
  top: 25%;
}
.gallery-heart:nth-child(2) {
  left: 15%;
  top: 65%;
}
.gallery-heart:nth-child(3) {
  left: 35%;
  top: 10%;
}
.gallery-heart:nth-child(4) {
  left: 60%;
  top: 20%;
}
.gallery-heart:nth-child(5) {
  left: 80%;
  top: 50%;
}
.gallery-heart:nth-child(6) {
  left: 90%;
  top: 15%;
}
.gallery-heart:nth-child(7) {
  left: 55%;
  top: 75%;
}
.gallery-heart:nth-child(8) {
  left: 25%;
  top: 40%;
}

@keyframes heartFloat {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-18px);
  }
}

@media (max-width: 760px) {
  .gallery-cards {
    grid-auto-flow: column;
    grid-auto-columns: minmax(220px, 80vw);
    overflow-x: auto;
    scroll-snap-type: x mandatory;
    padding-bottom: 12px;
  }
  .gallery-card {
    scroll-snap-align: center;
  }
}
</style>
