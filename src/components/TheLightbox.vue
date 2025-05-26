<template>
  <div
    v-show="$props.isModalOpen"
    class="fixed top-0 left-0 w-dvw h-dvh bg-ui-dark-blue/50 z-10"
  >
    <div class="w-1/3 mt-18 mx-auto">
      <div class="relative">
        <img :src="selectedImg" alt="" class="rounded-xl" />
        <button
          @click="$emit('closeModal')"
          class="absolute -top-4 right-0 -translate-y-full"
        >
          <svg
            class="size-4 fill-ui-primary"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="m11.596.782 2.122 2.122L9.12 7.499l4.597 4.597-2.122 2.122L7 9.62l-4.595 4.597-2.122-2.122L4.878 7.5.282 2.904 2.404.782l4.595 4.596L11.596.782Z"
              fill-rule="evenodd"
            />
          </svg>
        </button>
        <button
          class="absolute rounded-full left-0 top-1/2 -translate-y-1/2 -translate-x-1/2 bg-white p-2 disabled:opacity-50"
          :disabled="isPrevDisabled"
          @click="prev"
        >
          <svg
            class="size-5 stroke-ui-dark-blue hover:stroke-ui-primary"
            viewBox="-5 -2 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path fill="none" stroke-width="3" d="M11 1 3 9l8 8" />
          </svg>
        </button>
        <button
          class="absolute rounded-full right-0 top-1/2 -translate-y-1/2 translate-x-1/2 bg-white p-2 disabled:opacity-50"
          :disabled="isNextDisabled"
          @click="next"
        >
          <svg
            class="size-5 stroke-ui-dark-blue hover:stroke-ui-primary"
            viewBox="-5 -2 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path fill="none" stroke-width="3" d="m2 1 8 8-8 8" />
          </svg>
        </button>
      </div>
      <ul class="flex gap-8 pt-4">
        <li
          v-for="img in imgs"
          :key="img.id"
          @click="selectActiveImg(img.id)"
          class="grow-0 md:grow shrink-0 md:shrink basis-full lg:border-2 md:rounded-xl md:overflow-hidden"
          :class="[
            isImgActive(img.id)
              ? 'lg:border-ui-primary'
              : 'lg:border-transparent',
          ]"
        >
          <img
            :src="[img.url]"
            alt=""
            :class="[isImgActive(img.id) ? 'lg:w-full' : '']"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

defineProps(['isModalOpen']);

defineEmits(['closeModal']);

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

const activeImg = ref(1);

function selectActiveImg(id) {
  activeImg.value = id;
}

function isImgActive(id) {
  return id === activeImg.value;
}

const selectedImg = computed(() => {
  const img = imgs.value.find((img) => img.id === activeImg.value);
  return img.url;
});

const isPrevDisabled = computed(() => {
  return activeImg.value === 1;
});

const isNextDisabled = computed(() => {
  return activeImg.value === imgs.value.length;
});

function next() {
  activeImg.value += 1;
}

function prev() {
  activeImg.value -= 1;
}
</script>
