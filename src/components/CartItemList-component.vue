<script setup>
import { inject } from 'vue'
import CartItem from './CartItem-component.vue'

const { cart, removeFromCart } = inject('cart')
</script>

<template>
  <div class="flex flex-col gap-4">
    <CartItem
      v-for="item in cart"
      :key="item.id"
      :title="item.title"
      :price="item.price"
      :imageUrl="item.imageUrl"
      @onClickRemove="removeFromCart(item)"
    />
  </div>
</template>
