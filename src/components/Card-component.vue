<script setup>
defineProps({
  title: String,
  imageUrl: String,
  price: Number,
  //  isFavorite: Boolean,
  isAdded: Boolean,
  onClickAdd: Function,
  //  onClickFavorite: Function,
})
</script>

<template>
  <div
    class="relative bg-white border border-gray-100 rounded-3xl p-8 transition hover:-translate-y-2 hover:shadow-xl hover:shadow-gray-200"
  >
    <!-- img
      :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'"
      alt="Like"
      class="absolute top-8 left-8"
      @click="onClickFavorite"
    / -->

    <img :src="imageUrl" alt="Sneaker" />
    <p class="mt-2">{{ title }}</p>

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-gray-400 uppercase">Цена:</span>
        <span class="font-bold">{{ price }} руб.</span>
      </div>

      <img
        class="cursor-pointer"
        :src="!isAdded ? '/plus.svg' : '/checked.svg'"
        alt="Plus"
        @click="onClickAdd"
      />
    </div>
  </div>
</template>
