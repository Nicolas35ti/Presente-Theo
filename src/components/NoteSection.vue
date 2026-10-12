<script setup>
defineProps({ title: { type: String, required: true } })
</script>

<template>
  <section class="note">
    <h2>{{ title }}</h2>
    <slot />
  </section>
</template>

<style scoped>
h2 {
  display: inline-block;
  margin-bottom: 8px;
  padding-bottom: 2px;
  font: 700 26px var(--font-hand);
  letter-spacing: 1px;
  color: var(--ink);
  border-bottom: 3px dashed var(--ink);
}
:slotted(p), :slotted(li) { font: 19px/1.35 var(--font-text); color: var(--ink-body); }
:slotted(ul) { list-style: none; }
:slotted(li)::before { content: '♡ '; color: var(--ink); }
</style>
