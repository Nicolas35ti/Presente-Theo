<script setup>
import { ref } from 'vue'

const emit = defineEmits(['opened'])
const open = ref(false)

const mascot = '/images/cinna-doodle.png'

function openCard() {
  if (open.value) return
  open.value = true
  setTimeout(() => emit('opened'), 1500) // espera o cartão abrir e avisa o App
}
const hide = (e) => (e.target.style.display = 'none')
</script>

<template>
  <div class="intro">
    <button class="card" :class="{ open }" aria-label="Abrir cartão" @click="openCard">
      <!-- parte de dentro (aparece quando abre) -->
      <span class="inside">
        <span class="inside-text">Para o Theo ♡</span>
      </span>

      <!-- capa que gira -->
      <span class="cover">
        <span class="face front">
          <img class="mascot" src="../images/cinna-cartao.gif" alt="" @error="hide" />
          <span class="hint">Clique para abrir</span>
        </span>
        <span class="face back"></span>
      </span>
    </button>
  </div>
</template>

<style scoped>
.intro {
  position: fixed;
  inset: 0;
  z-index: 20;
  display: grid;
  place-items: center;
}

.card {
  --w: min(280px, 42vw);
  position: relative;
  display: block;
  width: var(--w);
  height: calc(var(--w) * 1.35);
  padding: 0;
  border: 0;
  background: none;
  cursor: pointer;
  perspective: 1400px;
  transition: transform 1.1s ease;
  animation: float 3s ease-in-out infinite;
}
.card.open {
  animation: none;
  transform: translateX(calc(var(--w) / 2)); /* mantém o cartão aberto centralizado */
}
.card:focus-visible { outline: 3px solid #fff; outline-offset: 8px; }

/* dentro do cartão */
.inside {
  position: absolute;
  inset: 0;
  display: grid;
  place-items: center;
  border: 3px solid #fff;
  border-radius: 6px 16px 16px 6px;
  background-color: var(--paper);
  background-image: radial-gradient(var(--paper-dots) 1.2px, transparent 1.4px);
  background-size: 22px 22px;
  box-shadow: 0 0 30px rgba(255, 255, 255, 0.9), 0 12px 30px rgba(70, 130, 160, 0.35);
}
.inside-text { font: 700 30px var(--font-hand); color: var(--ink); }

/* capa */
.cover {
  position: absolute;
  inset: 0;
  display: block;
  transform-origin: left center;
  transform-style: preserve-3d;
  transition: transform 1.1s ease;
}
.card.open .cover { transform: rotateY(-170deg); }

.face {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 8px;
  border: 3px solid #fff;
  border-radius: 6px 16px 16px 6px;
  backface-visibility: hidden;
  box-shadow: 0 12px 30px rgba(70, 130, 160, 0.35);
}
.front { background: linear-gradient(160deg, #e6f5fc, #9fd3ea); }
.back  { background: #dff0f8; transform: rotateY(180deg); }

.mascot { width: 70%; height: 40%; object-fit: contain; }
.cloud { font-size: 40px; }
.hint { font: 700 22px var(--font-hand); color: var(--ink); letter-spacing: 1px; }

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-8px); }
}
</style>