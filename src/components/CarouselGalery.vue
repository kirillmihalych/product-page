<template>
  <div class="relative md:z-0 overflow-x-hidden lg:overflow-auto lg:p-18">
    <img
      class="hidden lg:block lg:rounded-xl"
      :src="selectedImg"
      alt=""
      @click="$emit('openLightbox')"
    />
    <ul
      ref="carousel"
      class="flex transition-transform lg:justify-between lg:gap-4 lg:p-0 lg:pt-6"
      :style="carouselStyle"
    >
      <li
        v-for="img in imgs"
        :key="img.id"
        @click="selectActiveImg(img.id)"
        class="grow-0 lg:grow shrink-0 lg:shrink lg:rounded-md lg:overflow-hidden basis-full lg:border-2"
        :class="[
          isImgActive(img.id)
            ? 'lg:border-ui-primary'
            : 'lg:border-transparent',
        ]"
      >
        <img
          :src="img.url"
          alt=""
          :class="[isImgActive(img.id) ? 'lg:opacity-50 lg:w-full' : '']"
        />
      </li>
    </ul>
    <button
      class="absolute left-2 top-1/2 -translate-y-1/2 bg-white size-10 rounded-full flex items-center justify-center disabled:opacity-50 lg:hidden"
      :disabled="isPrevDisabled"
      @click="prev"
    >
      <img src="../assets/images/icon-previous.svg" alt="" />
    </button>
    <button
      class="absolute right-2 top-1/2 -translate-y-1/2 bg-white size-10 rounded-full flex items-center justify-center disabled:opacity-50 lg:hidden"
      :disabled="isNextDisabled"
      @click="next"
    >
      <img src="../assets/images/icon-next.svg" alt="" />
    </button>
  </div>
</template>

<script setup>
import { ref, computed, useTemplateRef } from 'vue';

defineEmits(['openLightbox']);

const carousel = useTemplateRef('carousel');
const carouselPosX = ref(0);
const carouselStyle = computed(() => {
  return {
    transform: `translate3d(-${carouselPosX.value}px,0px,0px)`,
  };
});

const itemWidth = computed(() => {
  return carousel.value ? carousel.value.getBoundingClientRect().width : 0;
});

const isPrevDisabled = computed(() => {
  return carouselPosX.value === 0;
});

const isNextDisabled = computed(() => {
  return carouselPosX.value === itemWidth.value * 3;
});

function next() {
  carouselPosX.value += itemWidth.value;
}

function prev() {
  carouselPosX.value -= itemWidth.value;
}

const activeImg = ref(1);
function selectActiveImg(id) {
  activeImg.value = id;
}

function isImgActive(id) {
  return id === activeImg.value;
}

const imgs = ref([
  {
    id: 1,
    url: new URL('../assets/images/image-product-1.jpg', import.meta.url).href,
  },
  {
    id: 2,
    url: new URL('../assets/images/image-product-2.jpg', import.meta.url).href,
  },
  {
    id: 3,
    url: new URL('../assets/images/image-product-3.jpg', import.meta.url).href,
  },
  {
    id: 4,
    url: new URL('../assets/images/image-product-4.jpg', import.meta.url).href,
  },
]);

const selectedImg = computed(() => {
  const img = imgs.value.find((img) => img.id === activeImg.value);
  return img.url;
});

// modal
</script>
