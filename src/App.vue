<script setup>
import { ref } from 'vue'
import IntroCard from '@/components/IntroCard.vue'
import ProfileView from '@/views/ProfileView.vue'
import CornerDecor from '@/components/CornerDecor.vue'
import { profile } from '@/data/profile'

const opened = ref(false)
</script>

<template>
  <Transition name="intro">
    <IntroCard v-if="!opened" @opened="opened = true" />
  </Transition>

  <Transition name="site">
    <div v-if="opened">
      <ProfileView />
      <CornerDecor :src="profile.corner" :credit="profile.credit" />
    </div>
  </Transition>
</template>

<style>
/* cartão some aumentando e esmaecendo */
.intro-leave-active { transition: opacity 0.7s ease, transform 0.7s ease; }
.intro-leave-to { opacity: 0; transform: scale(1.15); }

/* site aparece suavemente */
.site-enter-active { transition: opacity 0.9s ease; }
.site-enter-from { opacity: 0; }
</style>