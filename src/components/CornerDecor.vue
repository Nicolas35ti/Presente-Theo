<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
const props = defineProps({
  src: String,
  credit: String,
  restartMs: { type: Number, default: 5000 } // duração do seu GIF em ms
})
const hide = (e) => (e.target.style.display = 'none')

const tick = ref(0)
let timer
onMounted(() => (timer = setInterval(() => tick.value++, props.restartMs)))
onUnmounted(() => clearInterval(timer))
</script>

<template>
  <img v-if="src" class="corner" :src="`${src}?t=${tick}`" alt="" @error="hide" />
  <p v-if="credit" class="credit">{{ credit }}</p>
</template>

<style scoped>
.corner { position: fixed; right: 6px; bottom: 0; width: 210px; z-index: 2; pointer-events: none; }
.credit { position: fixed; right: 14px; bottom: 8px; font-size: 12px; z-index: 3; text-shadow: var(--text-shadow); }
@media (max-width: 640px) { .corner { width: 120px; } }
</style>
