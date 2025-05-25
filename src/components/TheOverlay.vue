<template>
  <div v-show="isMenuOpen" class="fixed h-dvh w-dvw bg-ui-dark-blue/75"></div>
</template>

<script setup>
defineProps(['isMenuOpen']);
</script>
