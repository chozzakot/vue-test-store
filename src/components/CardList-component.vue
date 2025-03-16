<script setup>
import Card from './Card-component.vue'

defineProps({
  items: Array,
})

const emit = defineEmits(['addToCart'])
</script>

<template>
  <div class="grid grid-cols-4 gap-5 mt-10">
    <Card
      v-for="item in items"
      :key="item.id"
      :title="item.title"
      :imageUrl="item.imageUrl"
      :price="item.price"
      :isAdded="item.isAdded"
      :isFavorite="false"
      :onClickAdd="() => emit('addToCart', item)"
    />
  </div>
</template>
