<script setup>
import NotebookPage from '@/components/NotebookPage.vue'
import NoteSection from '@/components/NoteSection.vue'
import PhotoCard from '@/components/PhotoCard.vue'
import { profile } from '@/data/profile'
import ShoppingList from '@/components/ShoppingList.vue'
import PhotoGallery from '@/components/PhotoGallery.vue'
import SiteFooter from '@/components/SiteFooter.vue'
</script>

<template>
  <main class="profile">
    <NotebookPage :heading="profile.heading" :title="profile.title" :date="profile.date" :doodle="profile.doodle">
      <PhotoCard :src="profile.photo" />

      <NoteSection :title="profile.about.title">
  <p>{{ profile.about.text1 }}</p>

  <PhotoCard src="/images/desenho-theo.png" side="center" />

  <p>{{ profile.about.text2 }}</p>
</NoteSection>
<ShoppingList :title="profile.shopping.title" :items="profile.shopping.items" />
<PhotoGallery :title="profile.gallery.title" :photos="profile.gallery.photos" />
<SiteFooter />
    </NotebookPage>
  </main>
</template>

<style scoped>
.profile { position: relative; z-index: 1; max-width: 760px; margin: 0 auto; padding: 70px 16px 100px; }
</style>