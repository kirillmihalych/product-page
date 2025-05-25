<template>
  <div>
    <TheOverlay :is-menu-open="isMenuOpen" />
    <header
      class="flex items-center justify-between p-4 lg:border-b-2 border-ui-light-gray"
    >
      <div class="relative flex gap-4 items-center justify-between">
        <button class="mt-0.5 xl:hidden" @click="isMenuOpen = true">
          <img src="../assets/images/icon-menu.svg" alt="open menu" />
        </button>
        <img src="../assets/images/logo.svg" alt="shop logo" />
        <nav
          class="fixed xl:static top-0 h-dvh xl:h-fit min-w-fit w-2/3 xl:w-fit p-4 bg-white font-bold text-xl xl:text-sm text-ui-dark-blue xl:text-ui-dark-blue/50 transition-[left] duration-300"
          :class="[isMenuOpen ? 'left-0' : '-left-full']"
        >
          <button @click="isMenuOpen = false" class="mb-10 xl:hidden">
            <img src="../assets/images/icon-close.svg" alt="menu close btn" />
          </button>
          <ul class="flex flex-col xl:flex-row gap-4">
            <li>
              <a href="#"> Collections </a>
            </li>
            <li>
              <a href="#">Men</a>
            </li>
            <li>
              <a href="#">Women</a>
            </li>
            <li>
              <a href="#"> About </a>
            </li>
            <li>
              <a href="#"> Contact </a>
            </li>
          </ul>
        </nav>
      </div>
      <div class="flex gap-4 items-center">
        <button>
          <img src="../assets/images/icon-cart.svg" alt="" />
        </button>
        <img
          src="../assets/images/image-avatar.png"
          alt="avatar"
          class="size-6"
        />
      </div>
    </header>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import TheOverlay from '@/components/TheOverlay.vue';

const isMenuOpen = ref(false);
</script>
