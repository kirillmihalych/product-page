<template>
  <div class="h-dvh max-w-[1440px] mx-auto font-kumbh-sans">
    <TheNavbar />
    <TheLightbox
      :is-modal-open="isLightboxOpen"
      @close-modal="isLightboxOpen = false"
    />
    <div class="lg:grid lg:grid-cols-2">
      <CarouselGalery @open-lightbox="isLightboxOpen = true" />
      <div class="lg:p-18"></div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import TheNavbar from '@/components/TheNavbar.vue';
import TheLightbox from '@/components/TheLightbox.vue';
import CarouselGalery from '@/components/CarouselGalery.vue';

const isLightboxOpen = ref(false);
</script>
