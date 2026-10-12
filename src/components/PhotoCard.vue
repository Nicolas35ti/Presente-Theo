<script setup>
import { ref } from 'vue'
defineProps({
  src: { type: String, required: true },
  side: { type: String, default: 'right' } // 'right' ou 'left'
})
const failed = ref(false)
</script>

<template>
  <figure class="polaroid" :class="side">
    <span class="tape" aria-hidden="true"></span>
    <img v-if="!failed" :src="src" alt="Foto" @error="failed = true" />
    <div v-else class="empty">{{ src }}</div>
  </figure>
</template>

<style scoped>
.polaroid {
  position: relative;
  width: 250px;
  padding: 10px 10px 34px;
  background: #fff;
  border-radius: 4px;
  box-shadow: 0 6px 14px rgba(70, 130, 160, 0.35);
}
.right { float: right; margin: 0 0 18px 28px; transform: rotate(3deg); }
.left  { float: left;  margin: 0 28px 18px 0; transform: rotate(-3deg); }

.center {
  clear: both;           /* o texto para, a foto ocupa a linha inteira */
  display: block;
  margin: 28px auto;
  width: 260px;          /* pode aumentar, ex: 320px */
  transform: rotate(-1.5deg);
}

.tape {
  position: absolute;
  top: -12px; left: 50%;
  width: 70px; height: 22px;
  transform: translateX(-50%) rotate(-4deg);
  background: rgba(184, 169, 236, 0.65);
}
img {
  display: block;
  width: 100%;
  height: auto; /* mantém a proporção original, sem cortar */
}
.empty {
  display: grid;
  place-items: center;
  width: 100%;
  aspect-ratio: 3 / 4;
  background: #dff0f8;
  font: 16px/1.2 var(--font-text);
  color: var(--ink-body);
  text-align: center;
}

@media (max-width: 640px) {
  .right, .left, .center { float: none; display: block; margin: 0 auto 18px; width: 200px; }
}
</style>