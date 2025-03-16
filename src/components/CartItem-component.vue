<script setup>
const emit = defineEmits(['onClickRemove'])

defineProps({
  id: Number,
  title: String,
  imageUrl: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickAdd: Function,
  onClickFavorite: Function,
})
</script>

<template>
  <div class="flex items-center gap-4 bg-white border border-gray-100 rounded-2xl p-4">
    <img class="w-16 h-16" :src="imageUrl" :alt="title" />

    <div class="flex flex-col flex-1">
      <p class="mt-2">{{ title }}</p>
      <div class="flex justify-between mt-2">
        <span class="font-bold flex-1">{{ price }} руб.</span>
        <img
          @click="emit('onClickRemove')"
          class="opacity-50 hover:opacity-100 cursor-pointer"
          src="/close.svg"
        />
      </div>
    </div>
  </div>
</template>
