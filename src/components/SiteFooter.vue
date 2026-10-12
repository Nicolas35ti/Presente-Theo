<script setup>
defineProps({
  text: { type: String, default: 'feito com muito amor por' },
  author: { type: String, default: 'nicolas <3' }
})
</script>

<template>
  <footer class="footer">
    <span>{{ text }} {{ author }}</span>
  </footer>
</template>

<style scoped>
.footer {
  clear: both;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 6px;
  margin-top: 44px;
  padding-top: 14px;
  border-top: 3px dashed rgba(95, 143, 224, 0.45);
  font: 700 18px var(--font-hand);
  letter-spacing: 0.5px;
  color: var(--ink);
}
.heart {
  display: inline-block;
  font-size: 22px;
  color: #ff8fb1;
  animation: beat 1.4s ease-in-out infinite;
}
@keyframes beat {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.25); }
}
</style>