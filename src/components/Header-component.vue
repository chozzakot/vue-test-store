<script setup>
defineProps({
  openDrawer: Function,
  closeDrawer: Function,
  totalPrice: Number,
})
</script>

<template>
  <header class="flex justify-between border-b border-gray-100 px-10 py-8">
    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-10" />
      <div>
        <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
        <p class="text-gray-400">Магазин лучших кроссовок</p>
      </div>
    </div>

    <div
      @click="openDrawer"
      class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black"
    >
      <img src="/cart.svg" alt="Cart" />
      <b>{{ totalPrice }} руб.</b>
    </div>
  </header>
</template>
