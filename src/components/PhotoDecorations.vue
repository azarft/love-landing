<template>
  <div class="photo-decor-layer" aria-hidden="true">
    <div
      v-for="(image, index) in images"
      :key="image"
      class="photo-frame"
      :class="`photo-${index + 1}`"
      :style="`background-image: url(/${image})`"
    ></div>
  </div>
</template>

<script setup>
import { onMounted } from "vue";
import { gsap } from "gsap";

const images = ["image1.jpg", "image2.jpg", "image3.jpg", "image4.jpg"];

onMounted(() => {
  gsap.utils.toArray(".photo-frame").forEach((item, idx) => {
    gsap.to(item, {
      y: -18 - idx * 2,
      rotation: idx % 2 === 0 ? 3 : -3,
      duration: 4 + idx * 0.6,
      yoyo: true,
      repeat: -1,
      ease: "sine.inOut",
    });
  });
});
</script>

<style scoped>
.photo-decor-layer {
  position: absolute;
  inset: 0;
  min-height: 100%;
  pointer-events: none;
  z-index: 1;
}

.photo-frame {
  position: absolute;
  width: clamp(150px, 24vw, 230px);
  height: clamp(200px, 28vw, 300px);
  background-size: cover;
  background-position: center;
  border-radius: 28px 28px 46px 46px;
  border: 1px solid rgba(255, 255, 255, 0.75);
  box-shadow: 0 20px 50px rgba(255, 168, 214, 0.35),
    inset 0 0 40px rgba(255, 255, 255, 0.2);
  opacity: 0.96;
  transform: rotate(-2deg);
  overflow: hidden;
}

.photo-frame::before {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(120deg, rgba(255, 255, 255, 0.25), transparent 55%);
  mix-blend-mode: screen;
}

.photo-frame::after {
  content: "";
  position: absolute;
  inset: 10px;
  border-radius: 20px 20px 34px 34px;
  border: 1px solid rgba(255, 244, 250, 0.8);
  box-shadow: inset 0 0 20px rgba(255, 255, 255, 0.35);
  opacity: 0.7;
}

.photo-1 {
  left: 4%;
  top: 18vh;
  transform: rotate(-6deg);
}

.photo-2 {
  right: 6%;
  top: 85vh;
  transform: rotate(5deg);
}

.photo-3 {
  left: 10%;
  top: 170vh;
  transform: rotate(4deg);
}

.photo-4 {
  right: 8%;
  top: 245vh;
  transform: rotate(-5deg);
}

@media (max-width: 900px) {
  .photo-1 {
    left: 6%;
    top: 22vh;
  }
  .photo-2 {
    right: 4%;
    top: 95vh;
  }
  .photo-3 {
    left: 4%;
    top: 165vh;
  }
  .photo-4 {
    right: 5%;
    top: 235vh;
  }
}

@media (max-width: 640px) {
  .photo-frame {
    width: clamp(130px, 52vw, 200px);
    height: clamp(180px, 60vw, 240px);
    opacity: 0.88;
  }
  .photo-1 {
    left: 8%;
    top: 28vh;
  }
  .photo-2 {
    right: 8%;
    top: 92vh;
  }
  .photo-3 {
    left: 6%;
    top: 165vh;
  }
  .photo-4 {
    right: 10%;
    top: 230vh;
  }
}
</style>
