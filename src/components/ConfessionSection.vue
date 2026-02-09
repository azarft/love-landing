<template>
  <section class="section confession" :id="id">
    <div class="confession-card glass">
      <h2 class="section-title">Жүрөктөн чыккан сөздөр</h2>
      <p class="confession-text">{{ typedText }}</p>
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

const fullText =
  "Мээрим,\nСени биринчи жолу көргөн күндөн тартып жүрөгүм өзгөрдү.\nСенин жылмайганың — менин кубанычым.\nСенин көз карашың — менин демим.\nАзыр биз алыстабыз: мен Петербургдамын, сен Таласта, Кыргызстандасың.\nБирок жүрөгүм дайыма сенде.\nСен жанымда болгондо убакыт токтоп калгандай сезилет.\nМен сени чын жүрөгүм менен сүйөм.";

const typedText = ref("");

const typeText = () => {
  let idx = 0;
  const timer = setInterval(() => {
    typedText.value += fullText[idx];
    idx += 1;
    if (idx >= fullText.length) clearInterval(timer);
  }, 28);
};

onMounted(() => {
  gsap.from(".confession-card", {
    opacity: 0,
    y: 40,
    duration: 1.2,
    ease: "power3.out",
    scrollTrigger: {
      trigger: ".confession-card",
      start: "top 80%",
    },
  });
  ScrollTrigger.create({
    trigger: ".confession-card",
    start: "top 70%",
    once: true,
    onEnter: typeText,
  });
});
</script>

<style scoped>
.confession {
  display: flex;
  justify-content: center;
}

.confession-card {
  padding: 48px 32px;
  max-width: 720px;
  width: 100%;
}

.confession-text {
  white-space: pre-line;
  font-size: clamp(1.1rem, 2.6vw, 1.35rem);
  line-height: 1.8;
  margin: 0;
  color: #3a1b33;
}
</style>
