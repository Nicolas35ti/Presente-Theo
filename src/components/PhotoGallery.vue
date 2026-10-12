<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import NoteSection from '@/components/NoteSection.vue'

defineProps({
  title: { type: String, required: true },
  photos: { type: Array, default: () => [] }
})

const selected = ref(null) // foto aberta em tela cheia
const close = () => (selected.value = null)
const onKey = (e) => e.key === 'Escape' && close()

onMounted(() => window.addEventListener('keydown', onKey))
onUnmounted(() => window.removeEventListener('keydown', onKey))
</script>

<template>
  <NoteSection class="gallery" :title="title">
    <div class="grid">
      <figure
        v-for="(photo, i) in photos"
        :key="photo.src"
        class="polaroid"
        :class="i % 2 === 0 ? 'tilt-a' : 'tilt-b'"
      >
        <button class="open" :aria-label="'Ampliar: ' + photo.caption" @click="selected = photo">
          <span class="tape" aria-hidden="true"></span>
          <img :src="photo.src" :alt="photo.caption" loading="lazy" />
        </button>
        <figcaption>{{ photo.caption }}</figcaption>
      </figure>
    </div>

    <!-- foto ampliada -->
    <Teleport to="body">
      <Transition name="fade">
        <div v-if="selected" class="overlay" @click="close">
          <figure class="big" @click.stop>
            <img :src="selected.src" :alt="selected.caption" />
            <figcaption>{{ selected.caption }}</figcaption>
            <button class="close" aria-label="Fechar" @click="close">✕</button>
          </figure>
        </div>
      </Transition>
    </Teleport>
  </NoteSection>
</template>

<style scoped>
.gallery { clear: both; margin-top: 40px; }

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(190px, 1fr));
  gap: 30px 24px;
  padding-top: 10px;
}

.polaroid {
  position: relative;
  padding: 10px 10px 12px;
  background: #fff;
  border-radius: 4px;
  box-shadow: 0 6px 14px rgba(70, 130, 160, 0.3);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
}
.tilt-a { transform: rotate(-2deg); }
.tilt-b { transform: rotate(2deg); }
.polaroid:hover { transform: rotate(0) scale(1.04); box-shadow: 0 10px 20px rgba(70, 130, 160, 0.4); }

.open { display: block; width: 100%; padding: 0; border: 0; background: none; cursor: zoom-in; }
.open:focus-visible { outline: 3px solid var(--ink); outline-offset: 3px; }

.tape {
  position: absolute;
  top: -20px; left: 50%;
  width: 60px; height: 20px;
  transform: translateX(-50%) rotate(-4deg);
  background: rgba(184, 169, 236, 0.65);
}
img { display: block; width: 100%; aspect-ratio: 1; object-fit: cover; background: #dff0f8; }

figcaption {
  margin-top: 10px;
  font: 18px/1.2 var(--font-hand);
  font-weight: 700;
  color: var(--ink-body);
  text-align: center;
}

/* ampliada */
.overlay {
  position: fixed;
  inset: 0;
  z-index: 50;
  display: grid;
  place-items: center;
  padding: 20px;
  background: rgba(40, 80, 110, 0.55);
  backdrop-filter: blur(3px);
}
.big {
  position: relative;
  max-width: min(92vw, 640px);
  max-height: 92vh;
  padding: 12px 12px 16px;
  background: #fff;
  border-radius: 6px;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.35);
}
.big img { max-height: 72vh; width: 100%; aspect-ratio: auto; object-fit: contain; }
.big figcaption { font-size: 22px; }
.close {
  position: absolute; top: -14px; right: -14px;
  width: 34px; height: 34px;
  border: 2px solid #fff; border-radius: 50%;
  background: var(--ink); color: #fff;
  font-size: 16px; cursor: pointer;
}

.fade-enter-active, .fade-leave-active { transition: opacity 0.25s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }
</style>