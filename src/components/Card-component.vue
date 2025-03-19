<script setup>
defineProps({
  title: String,
  imageUrl: String,
  price: Number,
  isAdded: Boolean,
  onClickAdd: Function,
})
</script>

<template>
  <div
    class="relative flex flex-col justify-between bg-white border border-gray-100 rounded-3xl p-8 transition hover:-translate-y-2 hover:shadow-xl hover:shadow-gray-200"
  >
    <div>
      <img :src="imageUrl" alt="Sneaker" />
      <p class="mt-2">{{ title }}</p>
    </div>

    <div class="flex items-end justify-between mt-5">
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
