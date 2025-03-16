<script setup>
import CartItemList from './CartItemList-component.vue'

defineProps({
  closeDrawer: Function,
  totalPrice: Number,
})
</script>

<template>
  <div @click="closeDrawer" class="fixed z-10 top-0 left-0 h-full w-full bg-black opacity-70"></div>
  <div class="flex flex-col fixed z-20 right-0 top-0 bg-white w-96 h-full p-10">
    <h2 class="text-2xl font-bold mb-8">Корзина</h2>

    <CartItemList class="flex-1" />

    <div class="flex flex-col mt-5">
      <div>
        <div class="flex gap-1">
          <span>Итого:</span>
          <div class="flex-1 border-b border-dashed h-5"></div>
          <b>{{ totalPrice }} руб.</b>
        </div>
      </div>

      <button
        :disabled="totalPrice ? false : true"
        class="mt-5 transition bg-lime-500 py-4 w-full border border-gray-100 rounded-2xl font-medium text-white hover:bg-lime-600 active:bg-lime-700 disabled:bg-gray-400 cursor-pointer"
      >
        Оформить заказ
      </button>
    </div>
  </div>
</template>
