<script setup>
import NoteSection from '@/components/NoteSection.vue'
defineProps({
  title: { type: String, required: true },
  items: { type: Array, default: () => [] }
})
</script>

<template>
  <NoteSection class="shopping" :title="title">
    <ul class="list">
      <li v-for="item in items" :key="item.url">
        <a :href="item.url" target="_blank" rel="noopener noreferrer">
          <span class="box" aria-hidden="true"></span>
          <span class="name">{{ item.name }}</span>
          <span v-if="item.note" class="note">({{ item.note }})</span>
          <span class="go" aria-hidden="true">↗</span>
        </a>
      </li>
    </ul>
  </NoteSection>
</template>

<style scoped>
.shopping { clear: both; margin-top: 36px; }

.list { list-style: none; max-width: 520px; }
li { border-bottom: 2px dashed rgba(95, 143, 224, 0.45); }

a {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 8px 4px;
  font: 20px/1.2 var(--font-text);
  color: var(--ink-body);
  text-decoration: none;
  transition: transform 0.2s ease, color 0.2s ease;
}
a:hover, a:focus-visible { color: var(--ink); transform: translateX(4px); outline: none; }

.box {
  position: relative;
  flex: none;
  width: 18px;
  height: 18px;
  border: 2.5px solid var(--ink);
  border-radius: 5px;
  background: #fff;
}
a:hover .box::after, a:focus-visible .box::after {
  content: '✓';
  position: absolute;
  inset: -6px 0 0 1px;
  font: 700 20px var(--font-hand);
  color: var(--ink);
}

.note { font-size: 16px; opacity: 0.75; }
.go { margin-left: auto; font: 700 20px var(--font-hand); color: var(--ink); }
</style>