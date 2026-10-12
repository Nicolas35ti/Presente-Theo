<script setup>
defineProps({
  heading: String,
  title: { type: String, default: '' },
  date: { type: Array, default: () => ['', '', ''] },
  doodle: String
})
const hide = (e) => (e.target.style.visibility = 'hidden')
</script>

<template>
  <article class="paper">
    <h1 v-if="heading" class="heading">{{ heading }}</h1>
    <img v-if="doodle" class="doodle" :src="doodle" alt="" @error="hide" />

    <div class="body"><slot /></div>
  </article>
</template>

<style scoped>
.paper {
  position: relative;
  padding: 26px 34px 40px;
  background-color: var(--paper);
  background-image: radial-gradient(var(--paper-dots) 1.2px, transparent 1.4px);
  background-size: 22px 22px;
  background-position: 11px 11px;
  border: 3px solid #fff;
  border-radius: 20px;
  box-shadow:
    0 0 0 6px rgba(255, 255, 255, 0.55),
    0 0 40px rgba(255, 255, 255, 0.9),
    0 14px 34px rgba(70, 130, 160, 0.35);
}
.heading {
  text-align: center;
  font: 600 18px var(--font-ui);
  color: #1f3a52;
  margin-bottom: 18px;
}
.doodle {
  position: absolute;
  top: -22px;
  right: 18px;
  width: 190px;
  height: 110px;
  object-fit: contain;
  filter: drop-shadow(0 3px 4px rgba(70, 130, 160, 0.3));
}
.field {
  display: flex;
  align-items: flex-end;
  gap: 6px;
  margin-bottom: 18px;
  font-family: var(--font-hand);
  font-weight: 700;
  color: var(--ink);
}
.label { font-size: 24px; letter-spacing: 1px; line-height: 1; }
.line {
  flex: 0 1 380px;
  min-height: 26px;
  padding: 0 8px;
  border-bottom: 4px solid var(--ink);
  border-radius: 2px;
  font-size: 22px;
  line-height: 1.1;
}
.slot {
  min-width: 34px;
  padding: 0 4px;
  text-align: center;
  border-bottom: 4px solid var(--ink);
  font-size: 22px;
  line-height: 1.1;
}
.sep { font-size: 24px; line-height: 1; }
.body { margin-top: 34px; display: flow-root; }

@media (max-width: 640px) {
  .paper { padding: 22px 18px 30px; }
  .doodle { width: 120px; height: 70px; top: -16px; right: 8px; }
  .line { flex: 1 1 auto; }
}
</style>
